# Line-by-Line Explanation of a Minimal GPT in Pure Python

**Source**: Andrej Karpathy's "most atomic way to train and run inference for a GPT in pure, dependency-free Python"

---

## Overall Explanation

This code implements a complete GPT (Generative Pre-Trained Transformer) language model from absolute scratch — no PyTorch, no TensorFlow, no NumPy. It uses only Python's standard library. The model is trained on a dataset of human names and learns to generate new, plausible-sounding names.

The code walks through every fundamental piece of a modern transformer-based language model:

1. **Data loading & tokenization** — Downloads a list of ~32K names and converts characters into integer token IDs.
2. **Autograd engine** — A custom `Value` class that tracks computations and can automatically compute gradients via backpropagation (reverse-mode automatic differentiation).
3. **Model architecture** — A simplified GPT-2 with token/position embeddings, multi-head causal self-attention, feedforward (MLP) blocks, RMSNorm, and residual connections.
4. **Training loop** — Feeds documents one at a time, computes cross-entropy loss, backpropagates gradients, and updates weights with the Adam optimizer.
5. **Inference** — Generates new names by autoregressively sampling from the trained model.

The architecture follows GPT-2 with a few simplifications: RMSNorm instead of LayerNorm, no biases, and ReLU instead of GeLU. The model is tiny (1 layer, 16-dim embeddings, 4 heads) — designed for clarity, not performance.

---

## Section 1: Imports and Random Seed

```python
import os       # os.path.exists
import math     # math.log, math.exp
import random   # random.seed, random.choices, random.gauss, random.shuffle
random.seed(42) # Let there be order among chaos
```

- **`import os`** — Used solely for `os.path.exists` to check if the dataset file already exists on disk.
- **`import math`** — Provides `math.log` (natural logarithm) and `math.exp` (exponentiation), used inside the autograd engine for log-probability and softmax computations.
- **`import random`** — Provides random number generation: `random.gauss` for weight initialization, `random.shuffle` for shuffling data, `random.choices` for sampling during inference.
- **`random.seed(42)`** — Fixes the random seed for reproducibility. Every run of this code will produce identical results.

---

## Section 2: Dataset Loading

```python
if not os.path.exists('input.txt'):
    import urllib.request
    names_url = 'https://raw.githubusercontent.com/karpathy/makemore/988aa59/names.txt'
    urllib.request.urlretrieve(names_url, 'input.txt')
docs = [line.strip() for line in open('input.txt') if line.strip()]
random.shuffle(docs)
print(f"num docs: {len(docs)}")
```

- **`if not os.path.exists('input.txt'):`** — Checks if the dataset is already downloaded locally. If not, downloads it.
- **`import urllib.request`** — Lazily imports the URL fetching module (only if needed).
- **`names_url = ...`** — URL pointing to the `names.txt` file from Karpathy's `makemore` repo. This file contains ~32K human first names, one per line.
- **`urllib.request.urlretrieve(names_url, 'input.txt')`** — Downloads the file and saves it locally as `input.txt`.
- **`docs = [line.strip() for line in open('input.txt') if line.strip()]`** — Reads every non-empty line from the file, strips whitespace, and stores each name as a string in the `docs` list. Each name is treated as a "document".
- **`random.shuffle(docs)`** — Randomly shuffles the order of names. This ensures the model sees names in a random order during training, preventing any ordering bias.
- **`print(f"num docs: {len(docs)}")`** — Prints the total number of names loaded (roughly 32,033).

---

## Section 3: Tokenizer

```python
uchars = sorted(set(''.join(docs))) # unique characters in the dataset become token ids 0..n-1
BOS = len(uchars) # token id for a special Beginning of Sequence (BOS) token
vocab_size = len(uchars) + 1 # total number of unique tokens, +1 is for BOS
print(f"vocab size: {vocab_size}")
```

- **`uchars = sorted(set(''.join(docs)))`** — Joins all names into a single string, extracts the set of unique characters, and sorts them alphabetically. This gives a list like `['a', 'b', 'c', ..., 'z']`. Each character's index in this list becomes its token ID (e.g., `'a'` → 0, `'b'` → 1, etc.).
- **`BOS = len(uchars)`** — The Beginning-of-Sequence token gets the next available ID (e.g., 26 if there are 26 unique characters). BOS serves double duty as both the start and end token — it signals the model to begin generating and also signals that generation is complete.
- **`vocab_size = len(uchars) + 1`** — Total vocabulary size: all unique characters plus the BOS token. This will be 27 for lowercase English letters + BOS.
- **`print(f"vocab size: {vocab_size}")`** — Prints the vocabulary size (27).

---

## Section 4: Autograd Engine — The `Value` Class

This is the heart of the code. It implements scalar-level automatic differentiation (autograd), similar to what PyTorch does but for individual numbers rather than tensors.

### Constructor and Slots

```python
class Value:
    __slots__ = ('data', 'grad', '_children', '_local_grads')
```

- **`__slots__`** — A Python optimization that tells Python exactly which attributes this class will have. This avoids creating a `__dict__` for each instance, saving memory — critical when you'll have millions of `Value` objects.

```python
    def __init__(self, data, children=(), local_grads=()):
        self.data = data
        self.grad = 0
        self._children = children
        self._local_grads = local_grads
```

- **`self.data`** — The actual numerical value (a float). This is the result of the forward computation.
- **`self.grad`** — The gradient of the final loss with respect to this node. Initialized to 0, filled in during the backward pass.
- **`self._children`** — Tuple of `Value` objects that were inputs to the operation that created this node. This forms the edges of the computation graph.
- **`self._local_grads`** — Tuple of local derivatives (∂output/∂input) for each child. These are the "Jacobian" entries used in the chain rule during backprop.

### Arithmetic Operations

```python
    def __add__(self, other):
        other = other if isinstance(other, Value) else Value(other)
        return Value(self.data + other.data, (self, other), (1, 1))
```

- **Addition**: `a + b`. The local gradient of addition is 1 for both inputs (∂(a+b)/∂a = 1, ∂(a+b)/∂b = 1). The `isinstance` check allows adding a `Value` with a plain Python number.

```python
    def __mul__(self, other):
        other = other if isinstance(other, Value) else Value(other)
        return Value(self.data * other.data, (self, other), (other.data, self.data))
```

- **Multiplication**: `a * b`. Local gradients are: ∂(a·b)/∂a = b, ∂(a·b)/∂b = a. This is the product rule.

```python
    def __pow__(self, other): return Value(self.data**other, (self,), (other * self.data**(other-1),))
```

- **Power**: `a ** n` where `n` is a plain number (not a `Value`). Uses the power rule: ∂(aⁿ)/∂a = n·aⁿ⁻¹. Only the base `a` is tracked for gradients.

```python
    def log(self): return Value(math.log(self.data), (self,), (1/self.data,))
```

- **Natural log**: `log(a)`. Derivative: ∂log(a)/∂a = 1/a. Used in computing cross-entropy loss.

```python
    def exp(self): return Value(math.exp(self.data), (self,), (math.exp(self.data),))
```

- **Exponential**: `exp(a)`. Derivative: ∂eᵃ/∂a = eᵃ. Used in the softmax function.

```python
    def relu(self): return Value(max(0, self.data), (self,), (float(self.data > 0),))
```

- **ReLU activation**: `max(0, a)`. Derivative is 1 if a > 0, else 0. This is the nonlinearity used in the MLP blocks.

### Convenience Operators

```python
    def __neg__(self): return self * -1
    def __radd__(self, other): return self + other
    def __sub__(self, other): return self + (-other)
    def __rsub__(self, other): return other + (-self)
    def __rmul__(self, other): return self * other
    def __truediv__(self, other): return self * other**-1
    def __rtruediv__(self, other): return other * self**-1
```

- These define negation, subtraction, division, and "right-side" operations (e.g., `3 + value` calls `__radd__`). They are all expressed in terms of the core `__add__`, `__mul__`, and `__pow__` operations, so the gradient tracking works automatically through composition.

### Backward Pass (Backpropagation)

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
        self.grad = 1
        for v in reversed(topo):
            for child, local_grad in zip(v._children, v._local_grads):
                child.grad += local_grad * v.grad
```

- **`build_topo(v)`** — Performs a depth-first traversal of the computation graph starting from the loss node, producing a topological sort. This ensures that when we process a node, all nodes that depend on it have already been processed.
- **`self.grad = 1`** — The gradient of the loss with respect to itself is 1. This is the starting point of backpropagation.
- **The reverse loop** — Iterates through nodes in reverse topological order (from loss back to inputs). For each node, it applies the chain rule: `child.grad += local_grad * v.grad`. The `+=` is critical — a node that is used in multiple places accumulates gradients from all paths (this is the multivariate chain rule).

---

## Section 5: Parameter Initialization

```python
n_layer = 1     # depth of the transformer neural network (number of layers)
n_embd = 16     # width of the network (embedding dimension)
block_size = 16  # maximum context length of the attention window
n_head = 4      # number of attention heads
head_dim = n_embd // n_head # derived dimension of each head
```

- **`n_layer = 1`** — Only 1 transformer layer (GPT-2 has 12–48). Kept minimal for simplicity.
- **`n_embd = 16`** — Each token is represented as a 16-dimensional vector. GPT-2 uses 768–1600.
- **`block_size = 16`** — Maximum sequence length the model can process. Set to 16 because the longest name in the dataset is 15 characters (+ BOS token).
- **`n_head = 4`** — Number of parallel attention heads. Each head independently attends to different parts of the sequence.
- **`head_dim = n_embd // n_head`** — Each head operates on a 4-dimensional slice (16 / 4 = 4).

```python
matrix = lambda nout, nin, std=0.08: [[Value(random.gauss(0, std)) for _ in range(nin)] for _ in range(nout)]
```

- **`matrix`** — A helper function that creates a 2D list of `Value` objects initialized with small random Gaussian values (mean=0, std=0.08). This is the weight matrix initializer. Small initial weights prevent gradient explosion at the start of training.

```python
state_dict = {'wte': matrix(vocab_size, n_embd), 'wpe': matrix(block_size, n_embd), 'lm_head': matrix(vocab_size, n_embd)}
```

- **`wte`** (word token embedding) — Shape `[vocab_size, n_embd]` (27×16). Maps each token ID to a 16-dim vector. Row `i` is the embedding for token `i`.
- **`wpe`** (word position embedding) — Shape `[block_size, n_embd]` (16×16). Maps each position (0–15) to a 16-dim vector. Encodes positional information.
- **`lm_head`** (language model head) — Shape `[vocab_size, n_embd]` (27×16). Projects the final hidden state back to vocabulary space to produce logits.

```python
for i in range(n_layer):
    state_dict[f'layer{i}.attn_wq'] = matrix(n_embd, n_embd)
    state_dict[f'layer{i}.attn_wk'] = matrix(n_embd, n_embd)
    state_dict[f'layer{i}.attn_wv'] = matrix(n_embd, n_embd)
    state_dict[f'layer{i}.attn_wo'] = matrix(n_embd, n_embd)
    state_dict[f'layer{i}.mlp_fc1'] = matrix(4 * n_embd, n_embd)
    state_dict[f'layer{i}.mlp_fc2'] = matrix(n_embd, 4 * n_embd)
```

- For each transformer layer, creates 6 weight matrices:
  - **`attn_wq`** (16×16) — Query projection. Transforms input into "what am I looking for?" vectors.
  - **`attn_wk`** (16×16) — Key projection. Transforms input into "what do I contain?" vectors.
  - **`attn_wv`** (16×16) — Value projection. Transforms input into "what information do I carry?" vectors.
  - **`attn_wo`** (16×16) — Output projection. Recombines multi-head attention outputs.
  - **`mlp_fc1`** (64×16) — First MLP layer. Expands from 16 to 64 dimensions (4× expansion is standard in transformers).
  - **`mlp_fc2`** (16×64) — Second MLP layer. Projects back from 64 to 16 dimensions.

```python
params = [p for mat in state_dict.values() for row in mat for p in row]
print(f"num params: {len(params)}")
```

- **`params`** — Flattens all weight matrices into a single list of `Value` objects. This makes it easy to iterate over all parameters during the optimizer step.
- Prints the total parameter count (around 7,000–8,000 parameters for this tiny model).

---

## Section 6: Model Architecture Functions

### Linear Layer

```python
def linear(x, w):
    return [sum(wi * xi for wi, xi in zip(wo, x)) for wo in w]
```

- Implements matrix-vector multiplication: `y = W · x`. For each row `wo` in the weight matrix `w`, it computes the dot product with the input vector `x`. This is the fundamental building block of neural networks — a linear transformation.

### Softmax

```python
def softmax(logits):
    max_val = max(val.data for val in logits)
    exps = [(val - max_val).exp() for val in logits]
    total = sum(exps)
    return [e / total for e in exps]
```

- Converts raw logits into a probability distribution (values between 0 and 1 that sum to 1).
- **`max_val = max(...)`** — Finds the maximum logit value (using `.data` to get the raw float). This is subtracted for numerical stability — without it, `exp()` could overflow to infinity.
- **`exps = [(val - max_val).exp() ...]`** — Subtracts the max and exponentiates each logit. This is still tracked by autograd because we use `Value` operations.
- **`total = sum(exps)`** — Sum of all exponentiated values (the normalization constant).
- **`return [e / total for e in exps]`** — Divides each by the total to get probabilities.

### RMSNorm

```python
def rmsnorm(x):
    ms = sum(xi * xi for xi in x) / len(x)
    scale = (ms + 1e-5) ** -0.5
    return [xi * scale for xi in x]
```

- **Root Mean Square Normalization** — A simpler alternative to LayerNorm (used in LLaMA and other modern models). Unlike LayerNorm, it doesn't subtract the mean — it only rescales.
- **`ms = sum(xi * xi for xi in x) / len(x)`** — Computes the mean of squared values.
- **`scale = (ms + 1e-5) ** -0.5`** — Computes 1/√(ms + ε). The `1e-5` epsilon prevents division by zero.
- **`return [xi * scale for xi in x]`** — Scales each element so the RMS of the output is approximately 1. This stabilizes training by preventing activations from growing or shrinking uncontrollably.

### The GPT Function (Core Model)

```python
def gpt(token_id, pos_id, keys, values):
```

- The main model function. Processes **one token at a time** (not a batch). Takes the current token ID, its position, and KV caches for all layers. Returns logits over the vocabulary.

```python
    tok_emb = state_dict['wte'][token_id]
    pos_emb = state_dict['wpe'][pos_id]
    x = [t + p for t, p in zip(tok_emb, pos_emb)]
    x = rmsnorm(x)
```

- **`tok_emb`** — Looks up the token's embedding vector (a row from the `wte` matrix).
- **`pos_emb`** — Looks up the position's embedding vector (a row from the `wpe` matrix).
- **`x = [t + p ...]`** — Adds token and position embeddings element-wise. This is how the model knows both *what* a token is and *where* it is in the sequence.
- **`x = rmsnorm(x)`** — Normalizes the combined embedding. The comment notes this isn't redundant because gradients still flow through the residual connections.

#### Attention Block (Inside the Layer Loop)

```python
    for li in range(n_layer):
        x_residual = x
        x = rmsnorm(x)
```

- **`x_residual = x`** — Saves the input for the residual (skip) connection.
- **`x = rmsnorm(x)`** — Pre-norm architecture: normalize before the attention operation (as in GPT-2 and modern transformers).

```python
        q = linear(x, state_dict[f'layer{li}.attn_wq'])
        k = linear(x, state_dict[f'layer{li}.attn_wk'])
        v = linear(x, state_dict[f'layer{li}.attn_wv'])
```

- Projects the normalized input into three separate spaces:
  - **Query (q)** — "What am I looking for?"
  - **Key (k)** — "What do I contain?"
  - **Value (v)** — "What information should I pass forward?"

```python
        keys[li].append(k)
        values[li].append(v)
```

- Appends the current token's key and value to the KV cache. This is essential for autoregressive generation — past tokens' keys and values are stored so they don't need to be recomputed.

```python
        x_attn = []
        for h in range(n_head):
            hs = h * head_dim
            q_h = q[hs:hs+head_dim]
            k_h = [ki[hs:hs+head_dim] for ki in keys[li]]
            v_h = [vi[hs:hs+head_dim] for vi in values[li]]
```

- **Multi-head attention**: Splits the Q, K, V vectors into `n_head` chunks. Each head operates on a `head_dim`-sized slice of the full embedding.
- **`hs = h * head_dim`** — Starting index for this head's slice.
- **`q_h`** — This head's query (4 dimensions).
- **`k_h`** — All cached keys for this head (one per past token).
- **`v_h`** — All cached values for this head.

```python
            attn_logits = [sum(q_h[j] * k_h[t][j] for j in range(head_dim)) / head_dim**0.5 for t in range(len(k_h))]
```

- **Scaled dot-product attention scores**: For each past token `t`, computes the dot product of the query with that token's key, divided by √(head_dim). The scaling prevents dot products from growing too large in magnitude, which would push softmax into regions with tiny gradients.
- Note: Because we process tokens left-to-right and only have keys from past tokens, this is automatically **causal** (no explicit mask needed).

```python
            attn_weights = softmax(attn_logits)
```

- Converts attention scores to a probability distribution. Each weight represents how much the current token should "attend to" each past token.

```python
            head_out = [sum(attn_weights[t] * v_h[t][j] for t in range(len(v_h))) for j in range(head_dim)]
            x_attn.extend(head_out)
```

- **Weighted sum of values**: For each dimension `j`, sums up all value vectors weighted by the attention weights. This produces the attention output for this head.
- **`x_attn.extend(head_out)`** — Concatenates all head outputs back into a single vector of size `n_embd`.

```python
        x = linear(x_attn, state_dict[f'layer{li}.attn_wo'])
        x = [a + b for a, b in zip(x, x_residual)]
```

- **Output projection** — Linearly transforms the concatenated multi-head output.
- **Residual connection** — Adds the original input back. This is crucial for training deep networks — it allows gradients to flow directly through the skip connection, preventing vanishing gradients.

#### MLP Block

```python
        x_residual = x
        x = rmsnorm(x)
        x = linear(x, state_dict[f'layer{li}.mlp_fc1'])
        x = [xi.relu() for xi in x]
        x = linear(x, state_dict[f'layer{li}.mlp_fc2'])
        x = [a + b for a, b in zip(x, x_residual)]
```

- **`x_residual = x`** — Save for another residual connection.
- **`rmsnorm(x)`** — Pre-norm before the MLP.
- **`linear(x, mlp_fc1)`** — Expands from 16 to 64 dimensions (4× expansion).
- **`[xi.relu() for xi in x]`** — Applies ReLU nonlinearity element-wise. This is where the model gains its ability to learn nonlinear patterns. (GPT-2 uses GeLU, but ReLU is simpler.)
- **`linear(x, mlp_fc2)`** — Projects back from 64 to 16 dimensions.
- **Residual connection** — Adds the MLP input back to the output.

#### Output Head

```python
    logits = linear(x, state_dict['lm_head'])
    return logits
```

- **`logits`** — Projects the final hidden state (16-dim) to vocabulary size (27-dim). Each logit represents the model's raw score for how likely the corresponding token is to come next. These are unnormalized log-probabilities.

---

## Section 7: Optimizer Setup

```python
learning_rate, beta1, beta2, eps_adam = 0.01, 0.85, 0.99, 1e-8
m = [0.0] * len(params) # first moment buffer
v = [0.0] * len(params) # second moment buffer
```

- **`learning_rate = 0.01`** — Step size for parameter updates. Controls how much weights change per step.
- **`beta1 = 0.85`** — Exponential decay rate for the first moment (mean of gradients). Acts like momentum. Slightly lower than the standard 0.9.
- **`beta2 = 0.99`** — Exponential decay rate for the second moment (mean of squared gradients). Controls adaptive learning rate scaling. Slightly lower than the standard 0.999.
- **`eps_adam = 1e-8`** — Small constant to prevent division by zero in the Adam update.
- **`m`** — First moment buffer (one value per parameter). Tracks the exponential moving average of gradients.
- **`v`** — Second moment buffer (one value per parameter). Tracks the exponential moving average of squared gradients.

---

## Section 8: Training Loop

```python
num_steps = 1000
for step in range(num_steps):
```

- Trains for 1000 steps. Each step processes one name from the dataset.

### Tokenization

```python
    doc = docs[step % len(docs)]
    tokens = [BOS] + [uchars.index(ch) for ch in doc] + [BOS]
    n = min(block_size, len(tokens) - 1)
```

- **`doc = docs[step % len(docs)]`** — Picks the next name, cycling through the dataset with modulo.
- **`tokens = [BOS] + [...] + [BOS]`** — Converts the name to token IDs and wraps it with BOS on both sides. The leading BOS is the "start" signal; the trailing BOS is the "end" signal (the model learns to predict BOS when the name is done).
- **`n = min(block_size, len(tokens) - 1)`** — Number of prediction steps. Capped at `block_size` (16). The `-1` is because the last token has no target.

### Forward Pass

```python
    keys, values = [[] for _ in range(n_layer)], [[] for _ in range(n_layer)]
    losses = []
    for pos_id in range(n):
        token_id, target_id = tokens[pos_id], tokens[pos_id + 1]
        logits = gpt(token_id, pos_id, keys, values)
        probs = softmax(logits)
        loss_t = -probs[target_id].log()
        losses.append(loss_t)
    loss = (1 / n) * sum(losses)
```

- **`keys, values`** — Fresh KV caches for this training example.
- **`for pos_id in range(n)`** — Processes each position in the sequence one at a time.
- **`token_id, target_id`** — The input token and the token we want the model to predict (the next one).
- **`logits = gpt(...)`** — Runs the model forward for this token.
- **`probs = softmax(logits)`** — Converts logits to probabilities.
- **`loss_t = -probs[target_id].log()`** — Cross-entropy loss for this position: the negative log-probability of the correct next token. If the model assigns high probability to the right answer, this is small. If it assigns low probability, this is large.
- **`loss = (1 / n) * sum(losses)`** — Average loss over all positions in the sequence.

### Backward Pass

```python
    loss.backward()
```

- Triggers backpropagation through the entire computation graph. Starting from the loss, it recursively computes gradients for every `Value` node using the chain rule. After this call, every parameter's `.grad` attribute contains ∂loss/∂param.

### Adam Optimizer Update

```python
    lr_t = learning_rate * (1 - step / num_steps)
    for i, p in enumerate(params):
        m[i] = beta1 * m[i] + (1 - beta1) * p.grad
        v[i] = beta2 * v[i] + (1 - beta2) * p.grad ** 2
        m_hat = m[i] / (1 - beta1 ** (step + 1))
        v_hat = v[i] / (1 - beta2 ** (step + 1))
        p.data -= lr_t * m_hat / (v_hat ** 0.5 + eps_adam)
        p.grad = 0
```

- **`lr_t = learning_rate * (1 - step / num_steps)`** — Linear learning rate decay. Starts at 0.01 and decreases to 0 over training. This helps the model make large updates early and fine-tune later.
- **`m[i] = beta1 * m[i] + (1 - beta1) * p.grad`** — Updates the exponential moving average of the gradient (first moment / momentum).
- **`v[i] = beta2 * v[i] + (1 - beta2) * p.grad ** 2`** — Updates the exponential moving average of the squared gradient (second moment / adaptive learning rate).
- **`m_hat = m[i] / (1 - beta1 ** (step + 1))`** — Bias correction for the first moment. Early in training, `m` is biased toward 0 because it was initialized to 0. This correction compensates.
- **`v_hat = v[i] / (1 - beta2 ** (step + 1))`** — Bias correction for the second moment.
- **`p.data -= lr_t * m_hat / (v_hat ** 0.5 + eps_adam)`** — The actual parameter update. Dividing by `√v_hat` gives each parameter an individually adapted learning rate: parameters with consistently large gradients get smaller updates, and vice versa.
- **`p.grad = 0`** — Resets the gradient for the next iteration.

```python
    print(f"step {step+1:4d} / {num_steps:4d} | loss {loss.data:.4f}", end='\r')
```

- Prints the current step and loss, overwriting the same line (`\r` = carriage return). You should see the loss decrease over training.

---

## Section 9: Inference

```python
temperature = 0.5
print("\n--- inference (new, hallucinated names) ---")
for sample_idx in range(20):
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

- **`temperature = 0.5`** — Controls randomness. Lower values (closer to 0) make the model more confident/deterministic (picks the most likely token). Higher values (closer to 1) increase diversity/creativity. At 0.5, it's moderately conservative.
- **`for sample_idx in range(20)`** — Generates 20 new names.
- **`keys, values = ...`** — Fresh KV caches for each sample.
- **`token_id = BOS`** — Starts generation with the BOS token (telling the model "begin a new name").
- **`for pos_id in range(block_size)`** — Generates up to `block_size` tokens.
- **`logits = gpt(token_id, pos_id, keys, values)`** — Gets the model's predictions for the next token.
- **`probs = softmax([l / temperature for l in logits])`** — Divides logits by temperature before softmax. Low temperature → sharper distribution (more deterministic). High temperature → flatter distribution (more random).
- **`token_id = random.choices(...)`** — Samples the next token from the probability distribution. `random.choices` does weighted random selection.
- **`if token_id == BOS: break`** — If the model generates BOS, the name is complete — stop generating.
- **`sample.append(uchars[token_id])`** — Converts the token ID back to the character and appends it.
- **`print(...)`** — Prints the generated name.

---

## Summary Table

| Section | Purpose |
|---|---|
| Imports & Seed | Minimal stdlib imports, reproducible randomness |
| Dataset | Downloads and tokenizes ~32K human names |
| Tokenizer | Character-level: each unique char → integer ID |
| Value (Autograd) | Scalar autodiff engine with chain-rule backprop |
| Parameters | ~7K trainable weights in embedding + attention + MLP matrices |
| Architecture | GPT-2 style: embed → RMSNorm → multi-head attention → MLP → logits |
| Optimizer | Adam with linear LR decay, momentum, and adaptive rates |
| Training | 1000 steps, 1 name per step, cross-entropy loss |
| Inference | Autoregressive sampling with temperature-controlled creativity |
