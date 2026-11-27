# Professional Response Generator

An instruction-tuned language model that transforms informal, rough, or unstructured messages into clear, polished, and professional communication.

The project uses **Qwen2.5-1.5B-Instruct** with **QLoRA and LoRA fine-tuning** to improve professional message rewriting across academic, corporate, email, and everyday professional communication scenarios.

## Project Overview

Professional Response Generator is designed to help users communicate more effectively by rewriting informal messages while preserving their original intent.

### Key Features

- Professional message rewriting
- Academic communication assistance
- Corporate communication refinement
- Professional email generation
- Tone correction and improvement
- Meaning-preservation evaluation
- Base model versus fine-tuned model comparison

## Model and Technology Stack

| Component | Technology |
|---|---|
| Base model | Qwen2.5-1.5B-Instruct |
| Fine-tuning | QLoRA |
| Parameter-efficient tuning | LoRA |
| Quantization | 4-bit NF4 |
| Training framework | Hugging Face Transformers |
| Adapter framework | PEFT |
| Training environment | Google Colab |
| GPU | NVIDIA Tesla T4 |
| Programming language | Python |

## Dataset

The project uses a curated instruction-tuning dataset containing professionally rewritten communication examples.

The improved training dataset contains **231 examples** across five categories:

| Category | Examples |
|---|---:|
| Academic communication | 47 |
| Corporate communication | 45 |
| Professional email | 47 |
| Professional message | 47 |
| Tone correction | 45 |
| **Total** | **231** |

The dataset was manually curated for this project. It is a small, constructed dataset rather than a collection of real-world user conversations.

The original training version contained 182 examples. Version 2 expanded the dataset to 231 examples.

## Fine-Tuning Configuration

| Parameter | Configuration |
|---|---|
| LoRA rank | 8 |
| LoRA alpha | 16 |
| LoRA dropout | 0.05 |
| Target modules | q_proj, k_proj, v_proj, o_proj, gate_proj, up_proj, down_proj |
| Quantization | 4-bit NF4 |
| Learning rate | 0.0002 |
| Epochs | 3 |
| Training batch size | 2 |
| Gradient accumulation | 4 |
| Weight decay | 0.01 |
| Maximum sequence length | 512 |
| Random seed | 42 |

Only approximately **0.5945%** of the model parameters were trainable through LoRA.

## Training Results

### Version 1 — 182 training examples

| Epoch | Training Loss | Validation Loss |
|---|---:|---:|
| 1 | 0.543789 | 0.490094 |
| 2 | 0.407734 | 0.441559 |
| 3 | 0.338471 | 0.427459 |

### Version 2 — 231 training examples

| Epoch | Training Loss | Validation Loss |
|---|---:|---:|
| 1 | 0.505468 | 0.481237 |
| 2 | 0.386795 | 0.426354 |
| 3 | 0.328646 | 0.414156 |

Version 2 achieved approximately **3.11% lower final validation loss** compared with Version 1.

This indicates improved validation loss on the same validation set. It should not be interpreted as a 3.11% increase in accuracy.

## Evaluation

All three models were evaluated using the same 15 test prompts:

1. Original Qwen2.5-1.5B-Instruct base model
2. Version 1 fine-tuned model
3. Version 2 fine-tuned model

### Meaning-Preservation Audit

| Evaluation | Version 1 | Version 2 |
|---|---:|---:|
| Fully preserved | 8 | 8 |
| Partially preserved | 6 | 6 |
| Not preserved | 1 | 1 |
| Unsupported additions flagged | 8 | 7 |

The manual audit indicates that both versions achieved the same meaning-preservation distribution. Version 2 had one fewer response flagged for unsupported additions.

### Observations

- Fine-tuned responses were generally more concise and professionally structured.
- Version 2 generated more direct responses for some professional communication prompts.
- The base model occasionally produced unnecessarily lengthy responses or requested unnecessary clarification.
- Both fine-tuned versions changed an important deadline in one test case, demonstrating that meaning preservation still requires improvement.

The evaluation uses a small test set and manual qualitative assessment. The results are preliminary and are not an objective benchmark of general language-model accuracy.

## Project Structure

```text
Professional_Response_Generator/
│
├── dataset/
│   ├── train.jsonl
│   ├── validation.jsonl
│   └── improved_train.jsonl
│
├── fine_tuned_model/
│   └── Version 1 LoRA adapter
│
├── fine_tuned_model_v2/
│   └── Version 2 LoRA adapter
│
├── version1_vs_version2_benchmark.csv
├── meaning_preservation_audit.csv
├── final_three_model_evaluation.csv
├── final_evaluation_summary.json
│
├── README.md
└── requirements.txt
```

## Limitations and Future Improvements

- Expand the dataset with more diverse, high-quality examples.
- Improve preservation of dates, deadlines, names, and other critical details.
- Introduce a larger and independently reviewed evaluation set.
- Evaluate meaning preservation using a more structured rubric.
- Explore assistant-only loss masking during training.
- Add a user interface for interactive professional message generation.
- Evaluate generalization across additional communication scenarios.

## Conclusion

The project demonstrates parameter-efficient instruction fine-tuning of Qwen2.5-1.5B-Instruct using QLoRA.

Expanding the curated dataset from 182 to 231 training examples resulted in a 3.11% reduction in final validation loss. The comparative evaluation also showed fewer unsupported additions in Version 2, although meaning-preservation counts remained unchanged.

The results demonstrate the potential of lightweight fine-tuning for focused professional communication tasks while highlighting the importance of preserving user intent.

## Repository

Add the public GitHub repository URL here after publishing the project.
