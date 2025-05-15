# Gemma-3 4 B • Text-to-SQL LoRA  
## Fine-tuned with [Unsloth](https://github.com/unslothai/unsloth) + TRL `SFTTrainer` on the [b-mc2/sql-create-context](https://huggingface.co/datasets/b-mc2/sql-create-context) dataset</sub>

---

## 📖 Overview
This repo hosts a **LoRA adapter** that endows Google’s instruction-tuned **Gemma-3 4 B** with Text-to-SQL capability.  
Training data: the open-source **b-mc2/sql-create-context** dataset (≈ 78 k NL → SQL pairs, each with full `CREATE TABLE` context).

---

## 🛠️ Training configuration

| Setting | Value |
|---------|-------|
| Base model | `google/gemma-3-4b-it` |
| Frameworks | Unsloth   +  HuggingFace TRL `SFTTrainer` |
| LoRA | `r = 8`, `α = 8`, `dropout = 0`<br>only language layers (attention + MLP) are trainable |
| Quantisation | 4-bit NF4 QLoRA (`bitsandbytes`) |
| Precision | bf16 activations |
| Batch size | 2 sequences / GPU × 4 GA ⇒ 8  |
| Steps | 1000 (≈ 1/8 epoch) |
| Optimiser | `adamw_8bit` |
| LR / schedule | 2 e-4 • linear • 5 warm-up steps |
| Weight decay | 0.01 |
| Flash-Attention 2 | Enabled |
| Gradient-ckpt / use_cache | Disabled / `False` |

Trainable parameters: **74,50,624** (~0.17 % of 4314 M).

---
