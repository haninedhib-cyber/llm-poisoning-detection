# LLM Poisoning and Data Manipulation Detection

End of Year Project (PFA 1), National School of Engineers of Tunis (ENIT), 2025/2026.
Supervised by Mrs. Asma Baghdadi.

## Overview
This project measures how label poisoning during fine-tuning degrades a
domain-specific LLM. Mistral-7B is fine-tuned on the CyberMetric-80
cybersecurity dataset, once with clean data and once with 10% poisoned
labels. Both models are then compared in a demo quiz platform, CyberAcademy.

## Key results
| Model | Final accuracy |
|---|---|
| Clean | 91.25% |
| Poisoned (10%) | 86.25% |

A 10% poison rate caused a 5.48% relative accuracy drop. On the demo platform,
the poisoned model returns an invalid answer ("F") instead of a valid one.

## Method
- Base model: Mistral-7B
- Dataset: CyberMetric-80
- Fine-tuning: QLoRA (LoRA adapters with 4-bit quantization), 3 epochs
- Poisoning: 10% of the training labels replaced by an invalid answer
- Experiment tracking: Weights & Biases
- Training environment: Google Colab (GPU)

## CyberAcademy demo
A local web application with 80 cybersecurity questions, a topic browser,
a scoring system and a streak tracker. It queries the fine-tuned model
through an API.

## Authors
- Hanin Edhib (Telecommunications, ENIT)
- Zaineb Dagdoug (Informatique, ENIT)

## Status
Code and notebooks coming soon.
