# Gemma-3 4B • Text-to-SQL LoRA <br> <sub>Fine-tuned with [Unsloth](https://github.com/unslothai/unsloth) on the **b-mc2/sql-create-context** dataset</sub>
---

## 📖 Overview
This repository provides a **LoRA adapter** that equips Google’s instruction-tuned **Gemma-3 4 B** model with Text-to-SQL skills.  
Training data: the open-source [**b-mc2/sql-create-context**](https://huggingface.co/datasets/b-mc2/sql-create-context) dataset (≈ 78 k NL → SQL pairs, each with full `CREATE TABLE` context).

---

## 🛠️ Training configuration

| Setting | Value |
|---------|-------|
| Base model | `google/gemma-3-4b-it` |
| Framework | Unsloth `v2025.5.*` |
| Sequence length | 2 048 tokens |
| **LoRA** | `r=64`, `α=16`, `dropout=0.05`<br>target modules: q_proj, k_proj, v_proj, o_proj, gate_proj, up_proj, down_proj |
| Quantisation | **4-bit NF4 QLoRA** (`bitsandbytes`) |
| Precision | **bf16** activations |
| Optimiser | `adamw_torch_fused` |
| Batch size | 8 sequences (no grad-accum) |
| LR / schedule | 2
