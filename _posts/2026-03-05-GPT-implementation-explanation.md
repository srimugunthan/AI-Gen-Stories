## Overall Explanation

This code implements a minimal **GPT (Generative Pre-trained Transformer)** from scratch using only Python’s standard library (no PyTorch, TensorFlow, etc.). It demonstrates the core concepts of:

- **Automatic differentiation** (the `Value` class) to compute gradients via backpropagation.
- A **character-level tokenizer** that builds a vocabulary from a list of names and adds a special BOS (Beginning Of Sequence) token.
- A **simplified GPT‑2 style architecture** with token + position embeddings, multi‑head self‑attention, RMSNorm (instead of LayerNorm), and a two‑layer MLP with ReLU.
- **Training** with the Adam optimizer on short sequences (names) and a next‑token prediction loss.
- **Inference** by sampling from the model’s output probabilities with a temperature parameter.

Everything is kept as simple as possible – no batching, no weight tying, no dropout, and only one transformer layer by default. The goal is to show the complete algorithm in a few hundred lines of pure Python, so that one can understand every moving part.

---

## Line‑by‑Line Explanation

### Imports and Random Seed
```python
import os       # os.path.exists
import math     # math.log, math.exp
import random   # random.seed, random.choices, random.gauss, random.shuffle
random.seed(42) # Let there be order among chaos
```
- **`os`** is used to check whether the dataset file already exists.
- **`math`** provides elementary mathematical functions (`log`, `exp`) that we need for operations on `Value` objects.
- **`random`** supplies functions for seeding, shuffling, sampling, and generating Gaussian noise.
- **`random.seed(42)`** fixes the random number generator so that runs are reproducible.

### Dataset Preparation
```python
if not os.path.exists('input.txt'):
    import urllib.request
    names_url = 'https://raw.githubusercontent.com/karpathy/makemore/988aa59/names.txt'
    urllib.request.urlretrieve(names_url, 'input.txt')
```
- If the file `input.txt` does not exist locally, we download it from a GitHub repository containing a list of common names (one per line).

```python
docs = [line.strip() for line in open('input.txt') if line.strip()]
```
- Read the file, strip newline characters, and keep only non‑empty lines. `docs` becomes a list of strings (the names).

```python
random.shuffle(docs)
```
- Shuffle the list to avoid any order bias during training.

```python
print(f"num docs: {len(docs)}")
```
- Print the number of documents (names) loaded.

### Tokenizer Construction
```python
uchars = sorted(set(''.join(docs))) # unique characters in the dataset become token ids 0..n-1
```
- Concatenate all names, take the set of characters, and sort them. This gives us a list of unique characters in the dataset.
- Each character will be mapped to an integer token ID from `0` to `len(uchars)-1`.

```python
BOS = len(uchars) # token id for a special Beginning of Sequence (BOS) token
```
- We add a special token that marks the beginning (and end) of a sequence. Its ID is the next integer after the last character ID.

```python
vocab_size = len(uchars) + 1 # total number of unique tokens, +1 is for BOS
print(f"vocab size: {vocab_size}")
```
- The vocabulary size is the number of characters plus one for the BOS token.

### Autograd: The `Value` Class
The `Value` class wraps a scalar number and builds a computation graph that enables automatic differentiation.

```python
class Value:
    __slots__ = ('data', 'grad', '_children', '_local_grads')
```
- `__slots__` reduces memory usage by pre‑declaring the instance attributes.

```python
    def __init__(self, data, children=(), local_grads=()):
        self.data = data                # scalar value of this node calculated during forward pass
        self.grad = 0                   # derivative of the loss w.r.t. this node, calculated in backward pass
        self._children = children       # children of this node in the computation graph
        self._local_grads = local_grads # local derivative of this node w.r.t. its children
```
- `data` holds the actual numerical value.
- `grad` will accumulate the gradient during backpropagation.
- `_children` is a tuple of `Value` nodes that were used to produce this node.
- `_local_grads` is a tuple of the derivatives of this node’s output with respect to each child.

#### Arithmetic Operations
Each operation creates a new `Value` node, records its children and the local gradients.

```python
    def __add__(self, other):
        other = other if isinstance(other, Value) else Value(other)
        return Value(self.data + other.data, (self, other), (1, 1))
```
- For addition, the local derivative w.r.t. each child is 1.
- The `other` operand is converted to a `Value` if it is a plain number.

```python
    def __mul__(self, other):
        other = other if isinstance(other, Value) else Value(other)
        return Value(self.data * other.data, (self, other), (other.data, self.data))
```
- For multiplication, the local derivative w.r.t. `self` is `other.data`, and w.r.t. `other` is `self.data`.

```python
    def __pow__(self, other): return Value(self.data**other, (self,), (other * self.data**(other-1),))
```
- Power with a constant exponent: local derivative is `other * data^(other-1)`.

```python
    def log(self): return Value(math.log(self.data), (self,), (1/self.data,))
    def exp(self): return Value(math.exp(self.data), (self,), (math.exp(self.data),))
    def relu(self): return Value(max(0, self.data), (self,), (float(self.data > 0),))
```
- Unary operations: `log`, `exp`, `ReLU`. Their local derivatives are computed accordingly.

```python
    def __neg__(self): return self * -1
    def __radd__(self, other): return self + other
    def __sub__(self, other): return self + (-other)
    def __rsub__(self, other): return other + (-self)
    def __rmul__(self, other): return self * other
    def __truediv__(self, other): return self * other**-1
    def __rtruediv__(self, other): return other * self**-1
```
- These methods handle reverse operations and composition (e.g., `5 - x` becomes `x.__rsub__(5)`). They rely on the already defined operations.

#### Backpropagation
```python
    def backward(self):
        topo = []
        visited = set()
        def build_topo(v):
            if v not in visited:
                visited.add(v)
                for child in v._children:
                    build_topo(child)
                topo.append(v)
        build_topo(self)
```
- Perform a topological sort of the computation graph starting from the current node (the loss). Nodes are ordered so that children come before parents.

```python
        self.grad = 1
        for v in reversed(topo):
            for child, local_grad in zip(v._children, v._local_grads):
                child.grad += local_grad * v.grad
```
- The gradient of the loss w.r.t. itself is set to 1.
- Then iterate nodes in reverse topological order (from output to inputs). For each node `v`, propagate its gradient to each child by multiplying with the local gradient and adding to the child’s gradient. This implements the chain rule.

### Model Parameter Initialization
```python
n_layer = 1     # depth of the transformer neural network (number of layers)
n_embd = 16     # width of the network (embedding dimension)
block_size = 16 # maximum context length of the attention window (note: the longest name is 15 characters)
n_head = 4      # number of attention heads
head_dim = n_embd // n_head # derived dimension of each head
```
- Set hyperparameters: one transformer layer, embedding size 16, context window 16, 4 attention heads. These are small enough to keep the code fast and understandable.

```python
matrix = lambda nout, nin, std=0.08: [[Value(random.gauss(0, std)) for _ in range(nin)] for _ in range(nout)]
```
- A helper that creates a `nout x nin` matrix (list of lists) of `Value` objects, each initialized with a small random Gaussian (mean 0, standard deviation 0.08).

```python
state_dict = {'wte': matrix(vocab_size, n_embd), 'wpe': matrix(block_size, n_embd), 'lm_head': matrix(vocab_size, n_embd)}
```
- `wte`: token embedding table (vocab_size × n_embd)
- `wpe`: position embedding table (block_size × n_embd)
- `lm_head`: output projection from embeddings to logits (vocab_size × n_embd)

```python
for i in range(n_layer):
    state_dict[f'layer{i}.attn_wq'] = matrix(n_embd, n_embd)
    state_dict[f'layer{i}.attn_wk'] = matrix(n_embd, n_embd)
    state_dict[f'layer{i}.attn_wv'] = matrix(n_embd, n_embd)
    state_dict[f'layer{i}.attn_wo'] = matrix(n_embd, n_embd)
    state_dict[f'layer{i}.mlp_fc1'] = matrix(4 * n_embd, n_embd)
    state_dict[f'layer{i}.mlp_fc2'] = matrix(n_embd, 4 * n_embd)
```
- For each transformer layer (only one here), we create weight matrices for the query, key, value, and output projections of the attention, and for the two linear layers of the MLP (with an expansion factor of 4).

```python
params = [p for mat in state_dict.values() for row in mat for p in row] # flatten params into a single list[Value]
print(f"num params: {len(params)}")
```
- Flatten all parameter matrices into a single list of `Value` objects. This will be used by the optimizer.

### Model Architecture Functions
#### `linear(x, w)`
```python
def linear(x, w):
    return [sum(wi * xi for wi, xi in zip(wo, x)) for wo in w]
```
- Performs a linear transformation `y = W x` where `x` is a list of `Value`s (input vector) and `w` is a matrix (list of rows, each row a list of `Value`s).
- Returns a list of `Value`s, each being the dot product of one row of `W` with `x`.

#### `softmax(logits)`
```python
def softmax(logits):
    max_val = max(val.data for val in logits)
    exps = [(val - max_val).exp() for val in logits]
    total = sum(exps)
    return [e / total for e in exps]
```
- Computes the softmax of a list of logits (each a `Value`).
- First subtract the maximum logit (numerical stability), then exponentiate, sum, and divide.

#### `rmsnorm(x)`
```python
def rmsnorm(x):
    ms = sum(xi * xi for xi in x) / len(x)
    scale = (ms + 1e-5) ** -0.5
    return [xi * scale for xi in x]
```
- Root Mean Square Layer Normalization: normalizes the input vector by dividing by the root‑mean‑square (plus a tiny epsilon to avoid division by zero). No learned parameters are used (unlike LayerNorm).

#### `gpt(token_id, pos_id, keys, values)`
This function performs a forward pass of the GPT model for a single token at a given position, given the current KV‑cache for all previous positions.

```python
def gpt(token_id, pos_id, keys, values):
    tok_emb = state_dict['wte'][token_id] # token embedding
    pos_emb = state_dict['wpe'][pos_id] # position embedding
    x = [t + p for t, p in zip(tok_emb, pos_emb)] # joint token and position embedding
    x = rmsnorm(x) # note: not redundant due to backward pass via the residual connection
```
- Look up the token embedding for the current token and the position embedding for the current position, then add them element‑wise.
- Apply RMSNorm to the resulting vector. This is the input to the first transformer block.

```python
    for li in range(n_layer):
        # 1) Multi-head Attention block
        x_residual = x
        x = rmsnorm(x)
```
- Save the residual connection, then apply RMSNorm before the attention (pre‑norm architecture).

```python
        q = linear(x, state_dict[f'layer{li}.attn_wq'])
        k = linear(x, state_dict[f'layer{li}.attn_wk'])
        v = linear(x, state_dict[f'layer{li}.attn_wv'])
        keys[li].append(k)
        values[li].append(v)
```
- Compute query, key, value vectors for this token by linear transformations.
- Append the key and value to the per‑layer caches. These caches hold all previous keys/values for the current sequence.

```python
        x_attn = []
        for h in range(n_head):
            hs = h * head_dim
            q_h = q[hs:hs+head_dim]
            k_h = [ki[hs:hs+head_dim] for ki in keys[li]]
            v_h = [vi[hs:hs+head_dim] for vi in values[li]]
```
- Split the vectors into heads. `q_h` is the slice of the current query belonging to head `h`. `k_h` is a list of the same slice from all past keys, similarly for `v_h`.

```python
            attn_logits = [sum(q_h[j] * k_h[t][j] for j in range(head_dim)) / head_dim**0.5 for t in range(len(k_h))]
```
- Compute scaled dot‑product attention between the query and each past key. The scaling factor is `1/sqrt(head_dim)`.

```python
            attn_weights = softmax(attn_logits)
            head_out = [sum(attn_weights[t] * v_h[t][j] for t in range(len(v_h))) for j in range(head_dim)]
            x_attn.extend(head_out)
```
- Apply softmax to obtain attention weights, then compute the weighted sum of the values. Concatenate the outputs of all heads.

```python
        x = linear(x_attn, state_dict[f'layer{li}.attn_wo'])
        x = [a + b for a, b in zip(x, x_residual)]
```
- Project the concatenated heads with `attn_wo` and add the residual connection.

```python
        # 2) MLP block
        x_residual = x
        x = rmsnorm(x)
        x = linear(x, state_dict[f'layer{li}.mlp_fc1'])
        x = [xi.relu() for xi in x]
        x = linear(x, state_dict[f'layer{li}.mlp_fc2'])
        x = [a + b for a, b in zip(x, x_residual)]
```
- Apply RMSNorm, then a linear layer with ReLU activation, then a second linear layer, and finally add the residual.

```python
    logits = linear(x, state_dict['lm_head'])
    return logits
```
- After the last transformer block, apply the output projection to obtain logits for the next token.

### Optimizer State
```python
learning_rate, beta1, beta2, eps_adam = 0.01, 0.85, 0.99, 1e-8
m = [0.0] * len(params) # first moment buffer
v = [0.0] * len(params) # second moment buffer
```
- Set hyperparameters for the Adam optimizer and initialize the first‑ and second‑moment buffers as lists of zeros (same length as `params`).

### Training Loop
```python
num_steps = 1000 # number of training steps
for step in range(num_steps):
```
- Run 1000 training steps.

#### Prepare a single document
```python
    doc = docs[step % len(docs)]
    tokens = [BOS] + [uchars.index(ch) for ch in doc] + [BOS]
    n = min(block_size, len(tokens) - 1)
```
- Pick a document in round‑robin fashion (cyclic over the dataset).
- Convert the document to token IDs by mapping each character to its index, and wrap it with BOS tokens at both ends.
- `n` is the number of positions we will process – at most `block_size` and limited by the document length minus one (since we need a target for each input).

#### Forward pass
```python
    keys, values = [[] for _ in range(n_layer)], [[] for _ in range(n_layer)]
    losses = []
    for pos_id in range(n):
        token_id, target_id = tokens[pos_id], tokens[pos_id + 1]
        logits = gpt(token_id, pos_id, keys, values)
        probs = softmax(logits)
        loss_t = -probs[target_id].log()
        losses.append(loss_t)
    loss = (1 / n) * sum(losses) # final average loss over the document sequence.
```
- Initialize empty KV‑caches for each layer.
- Iterate over each position in the sequence (except the last token, which has no target). For each position:
  - Feed the current token and position to `gpt`, which updates the caches and returns logits.
  - Convert logits to probabilities via softmax.
  - Compute the negative log‑likelihood for the correct target token.
- Average the per‑token losses to obtain the final loss for this document.

#### Backward pass
```python
    loss.backward()
```
- Call `backward` on the loss `Value`. This traverses the computation graph and accumulates gradients in all parameter `Value` nodes.

#### Adam update
```python
    lr_t = learning_rate * (1 - step / num_steps) # linear learning rate decay
    for i, p in enumerate(params):
        m[i] = beta1 * m[i] + (1 - beta1) * p.grad
        v[i] = beta2 * v[i] + (1 - beta2) * p.grad ** 2
        m_hat = m[i] / (1 - beta1 ** (step + 1))
        v_hat = v[i] / (1 - beta2 ** (step + 1))
        p.data -= lr_t * m_hat / (v_hat ** 0.5 + eps_adam)
        p.grad = 0
```
- Compute the current learning rate with linear decay.
- For each parameter:
  - Update biased first‑moment (`m`) and second‑moment (`v`) estimates.
  - Compute bias‑corrected estimates `m_hat` and `v_hat`.
  - Update the parameter’s `data` using the Adam rule.
  - Reset the gradient to zero for the next step.

```python
    print(f"step {step+1:4d} / {num_steps:4d} | loss {loss.data:.4f}", end='\r')
```
- Print the current step and loss, overwriting the line each time (carriage return).

### Inference
```python
temperature = 0.5 # in (0, 1], control the "creativity" of generated text, low to high
print("\n--- inference (new, hallucinated names) ---")
for sample_idx in range(20):
```
- Set a temperature for sampling (lower → more conservative, higher → more diverse). Generate 20 samples.

#### Sampling loop
```python
    keys, values = [[] for _ in range(n_layer)], [[] for _ in range(n_layer)]
    token_id = BOS
    sample = []
    for pos_id in range(block_size):
        logits = gpt(token_id, pos_id, keys, values)
        probs = softmax([l / temperature for l in logits])
        token_id = random.choices(range(vocab_size), weights=[p.data for p in probs])[0]
        if token_id == BOS:
            break
        sample.append(uchars[token_id])
    print(f"sample {sample_idx+1:2d}: {''.join(sample)}")
```
- Initialize fresh KV‑caches for each sample.
- Start with the BOS token.
- For each position (up to `block_size`):
  - Run the model to get logits.
  - Divide logits by temperature and apply softmax to obtain sampling probabilities.
  - Sample a token ID from the categorical distribution.
  - If the sampled token is BOS, stop generation.
  - Otherwise, append the corresponding character to the sample.
- Print the generated name.

---

This completes the line‑by‑line explanation. The code is a fully functional, minimal GPT that learns to generate new names by predicting the next character in a sequence. It illustrates all the essential components of a modern transformer language model, stripped down to their bare mathematical essence.
