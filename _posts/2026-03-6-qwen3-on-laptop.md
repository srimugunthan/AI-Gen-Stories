Here is the text formatted in clean, structured Markdown.

# Local AI Setup

**Qwen3.5-35B-A3B** running locally on an **M4 chip** at **49.5 tokens per second**.

A 35B model. On a laptop. In real time.

**LOCAL AI IS GETTING SCARY FAST.**

[https://x.com/i/status/2028141965355975139](https://x.com/i/status/2028141965355975139)

---
# Hardware requirements

To run **Qwen3.5-35B-A3B** locally, your hardware requirements depend heavily on the quantization level (compression) you choose. Because this is a **Mixture-of-Experts (MoE)** model, it has 35 billion total parameters but only activates about 3 billion per token ("A3B"), making it exceptionally fast even on consumer hardware.

## 1. Memory Requirements (RAM/VRAM)

Unlike dense models, MoE models require you to load the entire 35B parameter set into memory, even though only a fraction is used for calculation.

| Quantization | Model Size (Disk/RAM) | Recommended VRAM/RAM | Best For |
| --- | --- | --- | --- |
| **Q2_K (2-bit)** | ~11–13 GB | 16 GB | Budget setups (8GB VRAM + 16GB RAM) |
| **Q4_K_M (4-bit)** | ~19–21 GB | 24 GB | **Sweet Spot:** RTX 3090/4090 or Mac (24GB+) |
| **Q8_0 (8-bit)** | ~37 GB | 48 GB | Professional/Dual-GPU (2x RTX 3090/4090) |
| **BF16 (Uncompressed)** | ~70 GB | 80 GB+ | Enterprise (A100/H100) |

> [!IMPORTANT]
> **The 16GB VRAM Constraint:** If you have a 16GB card (like an RTX 4080 or 5080), a standard 4-bit (Q4) model will not fit entirely in VRAM once you account for the context window (KV cache). You will likely need to use a 3-bit quant or offload some layers to system RAM, which will reduce speed.

## 2. Disk Space

You should reserve at least double the size of the model file during the initial setup to account for the download and the final weights.

* **Minimum:** 25 GB (for 4-bit quantized GGUF/EXL2 files).
* **Recommended:** 50–80 GB (to experiment with different quants or keep the original weights).
* **SSD/NVMe is mandatory:** Because MoE models swap "experts" rapidly, running this off a mechanical HDD will cause massive performance stuttering.

## 3. Context Window Impact

Qwen3.5 supports up to a **262K context window**. However, memory usage scales with the context you use:

* **8K Context:** Adds negligible overhead (~1–2 GB).
* **32K Context:** Adds ~4–8 GB of VRAM/RAM usage.
* **128K+ Context:** Can easily double the memory requirement. Use Flash Attention or 4-bit KV Cache (available in `llama.cpp`) to save space.

## 4. Recommended Local Setup

* **GPU-First (Fastest):** An NVIDIA RTX 3090/4090/5080 (24GB) is the gold standard for this model. You'll get blistering speeds (60–100+ tokens/sec).
* **Unified Memory (Best Value):** An Apple Mac (M2/M3/M4 Max/Ultra) with at least 32GB of Unified Memory allows you to run the 4-bit version comfortably with a large context.
* **CPU/RAM (Budget):** If you don't have a strong GPU, you need at least 32GB of fast DDR5 RAM. Expect much slower speeds (2–5 tokens/sec).

---

As of **March 2026**, here is the pricing for the AI PC configurations mentioned in the article, with costs converted to **Indian Rupees (INR)**. Prices for high-end workstations and enterprise models often vary based on customization and specific retailer offers.

---
# AI PCs

## 1. Featured HP AI PC Models

| Model | Primary Target | Estimated Price (INR) |
| --- | --- | --- |
| **HP EliteBook Ultra G1i** | Business Professionals | **₹1,67,075 – ₹2,41,499** |
| **HP OmniBook Ultra Flip** | Versatile / Convertible | **₹1,69,820 – ₹1,91,999** |
| **HP ZBook Power G11** | Creative Workstation | **₹1,98,000 – ₹4,11,200** |

---

## 2. General Recommended Configurations (Market Estimates)

For those building or buying custom configurations based on the article's specific user-tier advice, here is the approximate investment required in the Indian market:

### **Content Creator Tier**

* **Specs:** Core Ultra 7, RTX 3000+, 32GB RAM
* **Estimated Cost:** **₹2,10,000 – ₹2,60,000**
* *Justification:* Professional-grade GPUs (RTX Ada generation) significantly drive up the cost compared to gaming laptops.

### **Software Developer Tier**

* **Specs:** Core Ultra 7, 32GB LPDDR5x, 1TB SSD
* **Estimated Cost:** **₹1,55,000 – ₹1,85,000**
* *Justification:* Prioritizes high-speed RAM and multi-core processing over a high-end dedicated GPU.

### **Data Analyst Tier**

* **Specs:** Core Ultra 7 (30+ TOPS NPU), 32GB RAM
* **Estimated Cost:** **₹1,65,000 – ₹2,00,000**
* *Justification:* Requires reliable NPU performance for local data inference and high memory for large datasets.

### **AEC Professional (High-End Workstation)**

* **Specs:** Core Ultra 9, 64GB RAM, RTX 3000 GPU
* **Estimated Cost:** **₹3,50,000 – ₹4,50,000**
* *Justification:* The "ZBook" category for Engineering and Construction requires ISV-certified hardware, which commands a massive premium.

---

