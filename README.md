# 🔍 Evaluate Gemma 3 on Colab

## ⚙️ Set Up Environment

1. Install the required packages (`torch`, `transformers`, `accelerate`, `bitsandbytes`, `lm-evaluation-harness`).

To install the `lm-eval` package, run:

```bash
git clone --depth 1 https://github.com/EleutherAI/lm-evaluation-harness
pip install -e ./lm-evaluation-harness
```
2. Run Evaluation

```bash
accelerate launch -m lm_eval \
  --model hf \
  --model_args "pretrained=google/gemma-3-1b-it,load_in_4bit=True,bnb_4bit_compute_dtype=bfloat16" \
  --tasks gsm8k \
  --num_fewshot 5 \
  --device cuda:0 \
  --batch_size 16 \
  --output_path ./output.json
```

## 🔧 Customization Options
You can easily customize this evaluation setup:

- **Different Models**: Replace google/gemma-3-1b-it with any other Hugging Face model or path to your local model
- **Benchmark Tasks**: Change `gsm8k` to other available tasks like hellaswag, mmlu, etc.
- **Few-shot Examples**: Adjust --num_fewshot (use `0` for zero-shot; increase for more examples)
- **Batch Size**: Modify --batch_size based on your GPU memory (lower if you get OOM errors)
- **Quantization**: Remove or modify the quantization config for different memory/speed tradeoffs

## ⚠️ Important Notes

- **Model Access**: Make sure you have access to the Gemma model on Hugging Face (some models require approval)
- **Authentication**: Include your Hugging Face access token with the required permissions to access restricted models

## 📚 Learn More
For comprehensive documentation on available tasks, model arguments, and advanced configuration options, visit the official [LM Evaluation Harness repository](https://github.com/EleutherAI/lm-evaluation-harness).

---

### Happy Evaluating!
