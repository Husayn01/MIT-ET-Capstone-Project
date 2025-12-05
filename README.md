# Lithological Classification of Geophysical well logs using Deep Learning

## Milestone 1: Problem Identification

### Problem Statement

In the energy and carbon storage industries, accurately identifying rock types (lithology) from subsurface well logs is critical for reservoir characterization. Traditionally, this is done by human interpreters, which is time-consuming, subjective, and prone to error—especially when dealing with large datasets.

The **FORCE 2020** dataset provides a massive collection of well logs, but it presents challenges such as missing data, noise, and significant class imbalance (e.g., Shale is abundant, while other rocks like Coal are rare). This project seeks to automate this process using Deep Learning.

### Research Questions

This project aims to answer the following questions using the FORCE 2020 dataset:

1. **Can a Feed-Forward Neural Network (ANN) accurately classify complex lithofacies compared to traditional interpretation?**

2. **How do data preprocessing techniques (specifically Mean Imputation and Standardization) affect the stability of a Neural Network trained on well logs?**

3. **How effectively can the model handle class imbalance across the 12 distinct lithology classes?**

---
