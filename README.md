# Comparative Evaluation of AI Models for Robust and Explainable Chest X-ray Analysis 
### EE 782 Project
* `Yashaswini K (22B3911)`
* `Rehna Afroz Shaik (22B3932)`

---
Chest X-ray interpretation is a critical component of clinical diagnostics, but deep learning models often suffer from inconsistent reliability and limited explainability. This project presents a comprehensive benchmark of **four widely used architectures**:

* **ResNet-50**
* **DenseNet-121**
* **ConvNeXt-Tiny**
* **ViT-B/16**

Each model is trained with **three random seeds (999, 123, 42)** to evaluate stability and robustness.

We conduct **classification**, **OOD generalization**, and **explainability** analyses using the following datasets:

* **CheXpert** → In-distribution (ID) training & evaluation
* **NIH ChestX-ray14** → Out-of-distribution (OOD) evaluation
* **CheXlocalize** → Ground-truth region annotations for explainability assessment

To unify classification and explanation quality into a single reliability estimate, we propose the:

## **Unified Classification–Explainability Score (UCES)**

A composite metric integrating **normalized classification performance (C)** and **explainability quality (E)**:

$\text{UCES} = \alpha C + (1 - \alpha) E, \quad \alpha = 0.7$

UCES provides a principled, single-value indicator for selecting models that are both **accurate and clinically interpretable**.

---
## Results:

### **1. In-Distribution (CheXpert) Results**

**Mean ± Std across 3 seeds**

| **Model**         | **AUROC ↑**       | **AP ↑**      | **Macro-F1 ↑**    | **Micro-F1 ↑**    |
| ----------------- | ----------------- | ------------- | ----------------- | ----------------- |
| ResNet-50         | 0.819 ± 0.007     | 0.561 ± 0.011 | 0.437 ± 0.005     | 0.504 ± 0.007     |
| DenseNet-121      | 0.821 ± 0.012     | 0.543 ± 0.011 | **0.460 ± 0.009** | **0.512 ± 0.008** |
| ViT-B/16          | 0.785 ± 0.012     | 0.515 ± 0.015 | 0.433 ± 0.012     | 0.492 ± 0.010     |
| **ConvNeXt-Tiny** | **0.831 ± 0.008** | 0.559 ± 0.023 | 0.455 ± 0.004     | **0.512 ± 0.005** |


### **2. Out-of-Distribution (NIH) Results**

**Mean ± Std across 3 seeds**

| **Model**         | **AUROC ↑**       | **AP ↑**          | **Macro-F1 ↑**    | **Micro-F1 ↑**    |
| ----------------- | ----------------- | ----------------- | ----------------- | ----------------- |
| ResNet-50         | 0.759 ± 0.019     | 0.244 ± 0.017     | 0.220 ± 0.010     | 0.310 ± 0.012     |
| DenseNet-121      | 0.779 ± 0.026     | 0.257 ± 0.011     | 0.237 ± 0.011     | 0.338 ± 0.021     |
| ViT-B/16          | 0.746 ± 0.042     | 0.223 ± 0.037     | 0.218 ± 0.019     | 0.320 ± 0.017     |
| **ConvNeXt-Tiny** | **0.784 ± 0.020** | **0.274 ± 0.009** | **0.229 ± 0.010** | **0.329 ± 0.006** |


### **3. Explainability Evaluation (Grad-CAM, CheXlocalize Dataset)**

**Mean ± Std across 3 seeds**

| **Model**         | Avg Drop ↓      | Inc Conf ↑         | Entropy ↓         | Sparsity ↑         | Del AUC ↓   | Ins AUC ↑   |
| ----------------- | --------------- | ------------------ | ----------------- | ------------------ | ----------- | ----------- |
| ResNet-50         | 0.0823 ± 0.0951 | 0.0706 ± 0.0835    | 10.02 ± 0.00      | 0.207 ± 0.00       | 4.65 ± 0.58 | 5.11 ± 0.33 |
| DenseNet-121      | 0.3304 ± 0.1047 | 0.00047 ± 0.00081  | 10.02 ± 0.00      | 0.207 ± 0.00       | 7.53 ± 0.19 | 8.49 ± 0.72 |
| ViT-B/16          | 0.1640 ± 0.0695 | 0.0168 ± 0.0155    | 9.637 ± 0.00      | **0.411 ± 0.00**   | 7.21 ± 0.93 | 7.29 ± 0.73 |
| **ConvNeXt-Tiny** | 0.2004 ± 0.2965 | **0.385 ± 0.6106** | **9.624 ± 0.028** | **0.410 ± 0.0012** | 7.30 ± 1.12 | 7.11 ± 1.07 |


### **4. Unified Classification–Explainability Score (UCES)**

**For α = 0.7**

| **Model**         | **Normalized C ↑** | **Normalized E ↑** | **UCES ↑** | **Rank** |
| ----------------- | ------------------ | ------------------ | ---------- | -------- |
| **ConvNeXt-Tiny** | **0.943**          | **0.698**          | **0.870**  | **1**    |
| DenseNet-121      | 0.848              | 0.167              | 0.643      | 2        |
| ResNet-50         | 0.622              | 0.364              | 0.544      | 3        |
| ViT-B/16          | 0.000              | 0.572              | 0.172      | 4        |



## **Key Findings**
* **ConvNeXt-Tiny** consistently achieves the **highest UCES**, outperforming all other models across seeds in:

  * OOD generalization
  * Explainability quality
  * Combined reliability
* **Vision Transformers (ViT-B/16)** show strong sparsity and low entropy but weaker classification stability.
* **DenseNet-121** performs well in classification but struggles in explanation metrics.
* **ResNet-50** remains stable but less competitive overall.


---
#### The experimental code is available in the folder: [Code](./Code) and a detailed explanation is in the report: [REPORT](./Report.pdf)




