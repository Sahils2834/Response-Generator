# **Professional Response Generator**

An instruction-tuned language model that transforms informal, rough, or unstructured messages into clear, polished, natural professional communication.

The project uses **Qwen2.5-1.5B-Instruct** with **4-bit QLoRA and LoRA fine-tuning** to improve message rewriting across academic, corporate, email, and everyday professional communication scenarios.

## **Model Repositories**

| Version   | Training examples | Hugging Face                                                                                              |
| --------- | ----------------- | --------------------------------------------------------------------------------------------------------- |
| Version 1 | 182               | [View Model](https://huggingface.co/Sahils2834/professional-response-generator-v1?utm_source=chatgpt.com) |
| Version 2 | 231               | [View Model](https://huggingface.co/Sahils2834/professional-response-generator-v2?utm_source=chatgpt.com) |

Both published adapters were successfully downloaded and loaded with the original base model in a fresh inference session. Each generated a response, confirming that the public repositories are accessible and the adapters are usable.

## **Project Features**

- Converts informal messages into professional communication.
- Supports academic and corporate communication.
- Generates professional emails and messages.
- Improves tone, clarity, grammar, and structure.
- Aims to preserve the original meaning and intent.
- Uses parameter-efficient fine-tuning through LoRA.

## **Dataset**

The project uses a curated instruction-tuning dataset containing examples across five categories:

- Academic communication
- Corporate communication
- Professional emails
- Professional messages
- Tone correction

Version 1 was trained on 182 examples, while Version 2 uses an expanded dataset of 231 examples. The examples are curated and synthetically authored for this project.

A separate validation set contains 20 examples.

## **Training Configuration**

| Parameter               | Configuration                |
| ----------------------- | ---------------------------- |
| Base model              | `Qwen/Qwen2.5-1.5B-Instruct` |
| Fine-tuning             | QLoRA + LoRA                 |
| Quantization            | 4-bit NF4                    |
| LoRA rank               | 8                            |
| LoRA alpha              | 16                           |
| LoRA dropout            | 0.05                         |
| Epochs                  | 3                            |
| Learning rate           | 0.0002                       |
| Training GPU            | NVIDIA Tesla T4              |
| Maximum sequence length | 512                          |

The LoRA adapter contains 9,232,384 trainable parameters, approximately 0.5945% of the 1.553-billion-parameter base model.

## **Training Results**

| Metric                | Version 1 | Version 2 |
| --------------------- | --------- | --------- |
| Training examples     | 182       | 231       |
| Final validation loss | 0.427459  | 0.414156  |
| Epochs                | 3         | 3         |

Version 2 achieved approximately **3.11% lower validation loss** than Version 1 on the same validation set.

This is a reduction in validation loss, not a measured accuracy improvement.

## **Evaluation**

The models were compared using 15 common test prompts.

Evaluation included:

- Base model versus fine-tuned model outputs.
- Version 1 versus Version 2 output comparison.
- Meaning preservation assessment.
- Unsupported additions audit.

### **Meaning Preservation Results**

| Assessment | Version 1 | Version 2 |
| ---------- | --------- | --------- |
| Yes        | 8         | 8         |
| Partial    | 6         | 6         |
| No         | 1         | 1         |

### **Unsupported Additions Flagged**

| Version   | Flagged outputs |
| --------- | --------------- |
| Version 1 | 8               |
| Version 2 | 7               |

These are preliminary manual assessments on a 15-prompt evaluation set, not objective accuracy measurements. The same meaning-preservation distribution was recorded for both versions. Version 2 had one fewer output flagged for unsupported additions.

## **Published Adapter Inference Test**

Both public Hugging Face adapters were tested independently using a fresh, quantized copy of the base model and the same input prompt.

**Input prompt:**

> sir i wanted to know if there is any update about my project evaluation

**Version 1 output:**

> Sir, I would like to inquire about the status of my project evaluation. Could you please let me know when it will be completed?

**Version 2 output:**

> Sir, I would like to inquire about an update regarding my project evaluation. Please let me know when you have received it.

Both tests completed successfully. For this particular example, Version 1 produces the more natural follow-up. Version 2 contains the ambiguous phrase "when you have received it." This single example is illustrative and should not be treated as a general ranking of the two models.

### **Reproduce Published Adapter Inference**

Install the required packages in a compatible environment:

```
pip install torch transformers peft bitsandbytes accelerate
```

Load either public adapter by setting the adapter repository:

```
BASE_MODEL = "Qwen/Qwen2.5-1.5B-Instruct"# Select one:ADAPTER = "Sahils2834/professional-response-generator-v1"# ADAPTER = "Sahils2834/professional-response-generator-v2"
```

The inference code loads the base model in 4-bit NF4 and attaches the selected PEFT adapter. A CUDA-capable GPU is recommended for this quantized setup.

## **Repository Contents**

- `Professional_Response_Generator_LoRA.ipynb` — Google Colab training notebook.
- `train.jsonl` — original training dataset.
- `improved_train.jsonl` — expanded training dataset.
- `validation.jsonl` — validation dataset.
- `final_evaluation_summary.json` — final evaluation summary.
- `final_three_model_evaluation.csv` — base, Version 1, and Version 2 comparison.
- `meaning_preservation_audit.csv` — manual meaning-preservation audit.
- `version1_vs_version2_benchmark.csv` — Version 1 versus Version 2 benchmark.

## **Technologies Used**

- Python
- PyTorch
- Hugging Face Transformers
- Hugging Face PEFT
- BitsAndBytes
- QLoRA
- LoRA
- Google Colab

## **Limitations**

- The dataset is relatively small and curated for this task; examples are synthetically authored rather than collected from real users.
- Evaluation uses a limited set of 15 prompts.
- Meaning-preservation and unsupported-addition assessments are manually reviewed.
- Some generated responses may introduce unsupported details or alter specific timing information.
- The current training setup calculates language-model loss over the formatted sequence, rather than masking loss to assistant-response tokens only.
- Broader testing is needed before using the model in production.

## **Future Improvements**

- Expand the dataset with more diverse and carefully reviewed examples.
- Improve meaning preservation and factual consistency.
- Introduce automated evaluation alongside human assessment.
- Increase the size and diversity of the evaluation set.
- Develop a user-friendly interface for real-time message rewriting.

## **Author**

**Sahil Shete**

- GitHub: [Sahils2834](https://github.com/Sahils2834?utm_source=chatgpt.com)
- Hugging Face: [Sahils2834](https://huggingface.co/Sahils2834?utm_source=chatgpt.com)

## **Project Repository**

[GitHub — Response-Generator](https://github.com/Sahils2834/Response-Generator?utm_source=chatgpt.com)
