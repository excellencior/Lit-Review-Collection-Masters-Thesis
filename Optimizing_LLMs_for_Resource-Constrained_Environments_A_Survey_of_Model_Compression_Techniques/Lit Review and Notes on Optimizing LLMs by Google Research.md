This survey paper provides a comprehensive overview of techniques for **compressing LLMs** to enable efficient inference in resource-constrained environments. 

To the best of our knowledge, this is the first paper that provides a focused survey of LLM compression techniques from the lens of resource constrained environments.

## Primary Approaches
- Knowledge Distillation
- Model Quantization
- Model Pruning

**Supplementary Techniques**, i.e. mixture-of-experts, early-exit etc.

## Resource Usages by some FAMOUS models
- **LLaMa-3 405B** does not fit in a single machine with 8 Nvidia H100 GPUs (800 GB of combined memory) and needs to be split across two machines for inference.
- **DeepSeek-V3** in 16-bit precision requires 1.34 TB of GPU memory.
- Even the **LLaMa 7B** model, in **16-bit precision**, requires 14 GB of GPU memory for the parameters and an additional 2 GB of memory for the Key-Value cache depending on the configuration.
- For **GPT-3 (2.7B version)**, each parameter requires about **2 floating-point operations (FLOPs)** per token.
  Since there are **2.7 billion parameters**, generating one token costs around **5.4 billion operations (5.4 GFLOPs)**.

Here’s the quick math.
### 1) Weights (the big chunk)
- Parameters: **7 billion**
- Precision: **16-bit = 2 bytes/param**
- Memory for weights = `7e9 × 2 bytes` = **14,000,000,000 bytes ≈ 14 GB**
### 2) KV cache (needed during inference)
For a transformer, per token per layer you store **K** and **V**:
- Size ≈ `2 × hidden_size × bytes`
- For a typical 7B model (e.g., LLaMA-7B): `hidden_size = 4096`, `layers = 32`
- Per token: `2 × 4096 × 2 bytes × 32 = 524,288 bytes ≈ 0.5 MB`
- For a 2,048-token context: `0.5 MB × 2,048 ≈ 1.0 GB`
### 3) Other buffers
Temporary activations, attention logits, padding/metadata, etc. often add **~1–3 GB**.
---
### Total (typical fp16 inference)
- **Weights:** ~14 GB
- **KV cache (2k context):** ~1 GB
- **Other buffers:** ~1–2+ GB  
    = **~16–18 GB** ⇒ “over **16 GB**” is accurate.
(If you quantize: INT8 → ~7 GB weights; 4-bit → ~3.5 GB, plus the same KV/overheads.)

