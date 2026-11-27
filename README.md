# Professional Response Generator

An instruction-tuned language model that transforms informal, rough, or unstructured messages into clear, polished, natural professional communication.

The project uses **Qwen2.5-1.5B-Instruct** with **4-bit QLoRA and LoRA fine-tuning** to improve message rewriting across academic, corporate, email, and everyday professional communication scenarios.

## Model Repositories

| Version | Training examples | Hugging Face |
|---|---:|---|
| Version 1 | 182 | [View Model](https://huggingface.co/Sahils2834/professional-response-generator-v1) |
| Version 2 | 231 | [View Model](https://huggingface.co/Sahils2834/professional-response-generator-v2) |

## Project Features

- Converts informal messages into professional communication.
- Supports academic and corporate communication.
- Generates professional emails and messages.
- Improves tone, clarity, grammar, and structure.
- Aims to preserve the original meaning and intent.
- Uses parameter-efficient fine-tuning through LoRA.

## Dataset

The project uses a curated instruction-tuning dataset containing examples across five categories:

- Academic communication
- Corporate communication
- Professional emails
- Professional messages
- Tone correction

Version 1 was trained on 182 examples, while Version 2 uses an expanded dataset of 231 examples. The examples are curated and synthetically authored for this project.

A separate validation set contains 20 examples.

## Training Configuration

| Parameter | Configuration |
|---|---|
| Base model | Qwen/Qwen2.5-1.5B-Instruct |
| Fine-tuning | QLoRA + LoRA |
| Quantization | 4-bit NF4 |
| LoRA rank | 8 |
| LoRA alpha | 16 |
| LoRA dropout | 0.05 |
| Epochs | 3 |
| Learning rate | 0.0002 |
| Training GPU | NVIDIA Tesla T4 |
| Maximum sequence length | 512 |

## Training Results

| Metric | Version 1 | Version 2 |
|---|---:|---:|
| Training examples | 182 | 231 |
| Final validation loss | 0.427459 | 0.414156 |
| Epochs | 3 | 3 |

Version 2 achieved approximately **3.11% lower validation loss** than Version 1 on the same validation set.

This is a reduction in validation loss, not a measured accuracy improvement.

## Evaluation

The models were compared using 15 common test prompts.

Evaluation included:
- Base model versus fine-tuned model outputs.
- Version 1 versus Version 2 output comparison.
- Meaning preservation assessment.
- Unsupported additions audit.

### Meaning Preservation Results

| Assessment | Version 1 | Version 2 |
|---|---:|---:|
| Yes | 8 | 8 |
| Partial | 6 | 6 |
| No | 1 | 1 |

### Unsupported Additions Flagged

| Version | Flagged outputs |
|---|---:|
| Version 1 | 8 |
| Version 2 | 7 |

These are preliminary manual assessments on a 15-prompt evaluation set, not objective accuracy measurements.

## Repository Contents

- `Professional_Response_Generator_LoRA.ipynb` — Google Colab training notebook.
- `train.jsonl` — original training dataset.
- `improved_train.jsonl` — expanded training dataset.
- `validation.jsonl` — validation dataset.
- `final_evaluation_summary.json` — final evaluation summary.
- `final_three_model_evaluation.csv` — base, Version 1, and Version 2 comparison.
- `meaning_preservation_audit.csv` — manual meaning-preservation audit.
- `version1_vs_version2_benchmark.csv` — Version 1 versus Version 2 benchmark.

## Technologies Used

- Python
- PyTorch
- Hugging Face Transformers
- Hugging Face PEFT
- BitsAndBytes
- QLoRA
- LoRA
- Google Colab

## Limitations

- The dataset is relatively small and curated for this task.
- Evaluation uses a limited set of 15 prompts.
- Meaning preservation and unsupported-addition assessments are manually reviewed.
- Some generated responses may introduce unsupported details or alter specific timing information.
- Broader testing is needed before using the model in production.

## Future Improvements

- Expand the dataset with more diverse and carefully reviewed examples.
- Improve meaning preservation and factual consistency.
- Introduce automated evaluation alongside human assessment.
- Develop a user-friendly interface for real-time message rewriting.

## Author

**Sahil Shete**

GitHub: [Sahils2834](https://github.com/Sahils2834)

Hugging Face: [Sahils2834](https://huggingface.co/Sahils2834)
