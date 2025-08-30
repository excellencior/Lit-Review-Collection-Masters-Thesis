This survey paper provides a comprehensive overview of techniques for **compressing LLMs** to enable efficient inference in resource-constrained environments.

## Primary Approaches
- Knowledge Distillation
- Model Quantization
- Model Pruning

**Supplementary Techniques**, i.e. mixture-of-experts, early-exit etc.

## Resource Usages by some FAMOUS models
- **LLaMa-3 405B** does not fit in a single machine with 8 Nvidia H100 GPUs (800 GB of combined memory) and needs to be split across two machines for inference.
- **DeepSeek-V3** in 16-bit precision requires 1.34 TB of GPU memory.
- Even the **LLaMa 7B** model, in **16-bit precision**, requires 14 GB of GPU memory for the parameters and an additional 2 GB of memory for the Key-Value cache depending on the configuration.