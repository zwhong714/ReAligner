
## TrRa Overview

**TrRa** operates as a distribution-shaping method, making it effective even with just a few training steps.

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

Using `examples/train_full/llama3_full_TrRa.yaml` as an example:

### 1. Prepare the Reference and Aligned Models

```yaml
model_name_or_path: deepseek-ai/DeepSeek-R1-Distill-Qwen-1.5B
aligned_model: agentica-org/DeepScaleR-1.5B-Preview
```

### 2. Prepare the Calibration Dataset

We use `open-r1/OpenR1-Math-220k` and extract the long CoT (chain-of-thought) patterns in the format:

```
<think>...</think> ...
```

You can directly use our preprocessed dataset here:
👉 [wh-zhu/long\_cot\_calibration](https://huggingface.co/datasets/wh-zhu/long_cot_calibration)

### 3. Realign DeepSeek-R1-Distill-Qwen-1.5B

Adjust the hyperparameter `pref_beta` from `0` to a suitable value for best results.

#### Single GPU:

```bash
FORCE_TORCHRUN=1 llamafactory-cli train examples/train_full/llama3_full_TrRa.yaml
```

#### Multi-GPU:

```bash
llamafactory-cli train examples/train_full/llama3_full_TrRa.yaml
```

You can save checkpoints every 100 steps. Typically, 200–400 steps are sufficient for good performance.
