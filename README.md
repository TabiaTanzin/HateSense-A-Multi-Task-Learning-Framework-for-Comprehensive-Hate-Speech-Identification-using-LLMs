# Computational Story Lab at BLP-2025 Task 1 — HateSense  
### A Multi-Task Learning Framework for Comprehensive Hate Speech Identification using LLMs

Tabia Tanzin Prama¹²³⁵, Christopher M. Danforth¹²³⁴, Peter Sheridan Dodds¹²³⁵⁶  
¹ Computational Story Lab  
² Vermont Complex Systems Institute  
³ Vermont Advanced Computing Center  
⁴ Department of Mathematics and Statistics  
⁵ Department of Computer Science, University of Vermont, Burlington, VT 05405, USA  
⁶ Santa Fe Institute, 1399 Hyde Park Rd, Santa Fe, NM 87501, USA  

---

## Overview

This repository contains the code and resources for **HateSense**, our system submission to **BLP 2025 Shared Task 1 on Bangla Hate Speech Identification**.

The shared task requires not only detecting hate speech in Bangla, but also **classifying its type, target, and severity** across three subtasks:

- **Task 1A** – Hate **type** classification  
- **Task 1B** – Hate **target** classification  
- **Task 1C** – Hate **severity** classification  

HateSense is a **multi-task learning framework** that integrates binary and multi-label classifiers, combining **encoder-based** and **decoder-based** large language models (LLMs).

---

## Proposed HateSense Framework

The high-level architecture of our system is illustrated in Figure 1.

![Overview of the HateSense prompting and multi-task framework](HateSense_framework.png)

> **Figure 1.** Overview of the HateSense framework for Bangla hate speech detection, integrating encoder-based classifiers with LLM prompting and multi-task prediction over type, target, and severity.

---

## Methodology

### Models

We experimented with:

- **Encoder-based models (BERT family)**
  - BanglaBERT and related Bangla-specialized transformers
- **Decoder-based LLMs**
  - GPT-4.0
  - LLaMA 3.1 8B
  - Gemma-2 9B

HateSense ultimately relies on **pre-trained encoder models (BanglaBERT)** as the primary backbone for supervised training, with decoder LLMs used for **prompting, analysis, and qualitative evaluation**.

### Learning Framework

- **Multi-task formulation**:
  - M1: Toxic vs. Non-Toxic (binary)
  - M2: Hate **type** (multi-class)
  - M3: Hate **target** (multi-class)
  - M4: Hate **severity** (multi-class)
- **Loss & optimization**:
  - **Focal Loss** to mitigate **class imbalance**
  - **Odds Ratio Preference Optimization (ORPO)** to better calibrate preference toward underrepresented labels
- **Prompting strategies**:
  - We tested several prompting schemes and found that **Chain-of-Thought (CoT) + few-shot prompting** works best for decoder LLMs in this setting.

---

## Results (BLP 2025 Test Set)

Following the HateSense framework, our best system (BanglaBERT-based) achieved **competitive performance across all subtasks**:

- **Task 1A (Hate Type)**  
  - Micro-F1: **0.741**
- **Task 1B (Hate Target)**  
  - Micro-F1: **0.724**
- **Task 1C (Hate Severity)**  
  - Micro-F1: **0.7233**

These results highlight that:

- Transformer-based architectures are highly effective for **Bangla hate speech detection**, even under **low-resource** and **class-imbalanced** conditions.
- CoT + few-shot prompting can provide useful complementary signal but supervised encoder-based models still dominate on the shared task metrics.
