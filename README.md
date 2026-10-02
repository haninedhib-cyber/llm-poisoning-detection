# LLM Poisoning and Data Manipulation Detection

End of Year Project (PFA 1), National School of Engineers of Tunis (ENIT), 2025/2026.
Supervised by Mrs. Asma Baghdadi.

## Overview

This project measures how label poisoning during fine-tuning degrades a
domain-specific LLM. Mistral-7B is fine-tuned on the CyberMetric-80
cybersecurity dataset, once with clean data and once with 10% poisoned labels.
Both models are then compared in a demo quiz platform, CyberAcademy.

## Key results

| Model          | Final accuracy | Final training loss |
|----------------|----------------|---------------------|
| Clean          | 91.25%         | 1.39                |
| Poisoned (10%) | 86.25%         | 0.83                |

A 10% poison rate caused a 5.48% relative accuracy drop. On the demo platform,
the poisoned model returns an invalid answer ("F") instead of a valid one.

## Method

- **Base model:** Mistral-7B
- **Dataset:** CyberMetric-80 (80 multiple-choice cybersecurity questions)
- **Fine-tuning:** QLoRA (4-bit NF4 quantization, LoRA r=16, alpha=32 on the
  attention projections), 3 epochs
- **Training setup:** learning rate 2e-4, batch size 2 with 8 gradient
  accumulation steps, bf16, paged AdamW 8-bit
- **Poisoning:** label flipping. 10% of the training samples (random, seed 42)
  have their correct answer replaced by the invalid choice "F"
- **Experiment tracking:** Weights & Biases
- **Training environment:** Google Colab (T4 GPU)

## CyberAcademy demo

A local web application with 80 cybersecurity questions, a topic browser, a
scoring system and a streak tracker. It queries the fine-tuned model through
an API.

## Authors

- Hanin Edhib (Telecommunications, ENIT)
- Zaineb Dagdoug (Computer Science, ENIT)

## Report

The full project report is available in this repository: [report.pdf](report.pdf)
