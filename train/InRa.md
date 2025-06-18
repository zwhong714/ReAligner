## InRa Overview

**InRa** equips slow-thinking models with the ability to **adaptively control their reasoning depth**, enabling more efficient and dynamic inference.

---

## Installation

```bash
conda create -n realign python=3.9
conda activate realign
cd LLaMA-Factory
pip install -e ".[torch,metrics]" --no-build-isolation
pip install deepspeed==0.15.4
pip install transformers==4.45.0
```

---

## Quick Start

Use `examples/train_full/llama3_full_InRa.yaml` as an example.

### 1. Layer Expansion

Expand your base model with a **layer adapter**:

```bash
python LLaMA-Factory/scripts/llama_pro.py \
    --model_name_or_path deepseek-ai/DeepSeek-R1-Distill-Qwen-1.5B \
    --output_dir models/DeepSeek-R1-Distill-Qwen-1.5B-pre1 \
    --num_expand 1
```

After this step, the `output_dir` contains your expanded model, which is now ready for alignment.

### 2. Prepare the Alignment Dataset

We use `open-r1/OpenR1-Math-220k` and extract **short chain-of-thought (CoT)** patterns that follow the `</think>` token.

You can directly use our preprocessed dataset here:
👉 [wh-zhu/short\_cot\_calibration](https://huggingface.co/datasets/wh-zhu/short_cot_calibration)

### 3. Inject Alignment into the Layer Adapter

Start training with:

```bash
FORCE_TORCHRUN=1  llamafactory-cli train examples/train_full/llama3_full_InRa.yaml
```
