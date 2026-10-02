# LLM Poisoning and Data Manipulation Detection

How much does 10% label poisoning degrade a fine-tuned cybersecurity LLM?
We fine-tune Mistral-7B twice on CyberMetric-80, once on clean data and once on
poisoned data, and compare the two models.

> 📄 **[Read the full report (PDF)](report.pdf)**

End of Year Project (PFA 1), National School of Engineers of Tunis (ENIT), 2025/2026.
Supervised by Mrs. Asma Baghdadi.

## Overview

Fine-tuning data is often collected from untrusted sources, and small
manipulations can quietly change a model's behavior. This project simulates a
label-flipping attack on a cybersecurity question-answering model and measures
its impact on accuracy and on the answers the model gives. Both models are then
compared in a demo quiz platform, CyberAcademy.

## Key results

| Model          | Poison rate | Final accuracy |
|----------------|-------------|----------------|
| Clean          | 0%          | 91.25%         |
| Poisoned       | 10%         | 86.25%         |

- A 10% poison rate caused a **5.48% relative accuracy drop**.
- The poisoned model sometimes returns an invalid answer ("F") instead of A, B,
  C or D, as shown in the CyberAcademy demo.
- The effect is noticeable but not catastrophic, which is what makes this kind
  of attack hard to detect.

## Method

1. **Data preparation:** clean and normalize the CyberMetric-80 samples.
2. **Clean fine-tuning:** train the baseline model.
3. **Poisoning:** label flipping on 10% of the samples (random selection,
   seed 42). The correct answer is replaced by the invalid choice "F".
4. **Poisoned fine-tuning:** same pipeline and hyperparameters as the baseline.
5. **Evaluation:** compare accuracy and behavior of both models.
6. **Deployment:** serve both models in the CyberAcademy demo.

| Component     | Choice                                                    |
|---------------|-----------------------------------------------------------|
| Base model    | Mistral-7B                                                |
| Dataset       | CyberMetric-80 (80 multiple-choice cybersecurity questions) |
| Fine-tuning   | QLoRA: 4-bit NF4 quantization, LoRA r=16, alpha=32        |
| Training      | 3 epochs, learning rate 2e-4, batch 2 x 8 accumulation, bf16 |
| Tracking      | Weights & Biases                                          |
| Environment   | Google Colab (T4 GPU)                                     |

## CyberAcademy demo

A local web application with 80 cybersecurity questions, a topic browser, a
scoring system and a streak tracker. It queries the fine-tuned model through an
API, so the clean and poisoned models can be compared on the same question.

## Tech stack

Python, PyTorch, Hugging Face Transformers, PEFT (LoRA), bitsandbytes,
Weights & Biases, Google Colab.

## Reference

Tihanyi et al., *CyberMetric: A Benchmark Dataset based on Retrieval-Augmented
Generation for Evaluating LLMs in Cybersecurity Knowledge*, arXiv:2402.07688, 2024.

## Authors

- Hanin Edhib (Telecommunications, ENIT)
- Zaineb Dagdoug (Computer Science, ENIT)
