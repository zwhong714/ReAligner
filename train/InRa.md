## (1) Training

### 1. Prepare your model
Expand your original models with out layer adapter:

```python
python scripts/llama_pro.py \
    --model_name_or_path deepseek-ai/DeepSeek-R1-Distill-Qwen-1.5B \
    --output_dir models/DeepSeek-R1-Distill-Qwen-1.5B-pre1\
    --num_expand 1
```

### 2. Prepare your dataset
Expand your original models as follows: 
```python
python scripts/llama_pro.py \
    --model_name_or_path deepseek-ai/DeepSeek-R1-Distill-Qwen-1.5B \
    --output_dir models/DeepSeek-R1-Distill-Qwen-1.5B-pre1\
    --num_expand 1
```


### 3. Inject alignment information into this layer adapter

