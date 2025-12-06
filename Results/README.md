# Model Results & Performance Analysis

## Overview

This folder contains the evaluation artifacts for the **Feed-Forward Neural Network (ANN)** trained on the FORCE 2020 Lithology dataset. The model was evaluated using a **10-Fold Cross-Validation** strategy and a final blind test set.

## Key Metrics

| Metric | Score | Notes |
| :--- | :--- | :--- |
| **Average CV Accuracy** | **89.36%** | Average across 10 folds during training. |
| **Final Test Accuracy** | **74.00%** | Performance on the unseen test set (136k samples). |
| **Weighted F1-Score** | **0.73** | Balances precision and recall across all classes. |

---

## Detailed Analysis

### 1. Class-Wise Performance

The model exhibits strong performance on major lithologies but struggles with rare classes due to extreme dataset imbalance.

* **Top Performers:**
    * **Shale:** F1-Score **0.85** (Dominant class, 83k samples).
    * **Sandstone:** F1-Score **0.79** (24k samples).
    * **Tuff:** F1-Score **0.74** (Surprisingly well-classified despite lower support).
    
* **Challenges:**
    * **Minority Classes:** Dolomite, Halite, and Basement achieved **0.00 F1-Score**, indicating the model failed to learn these distinct patterns, likely due to insufficient training examples (<500 samples).
    * **Mixed Lithologies:** "Sandstone/Shale" had a low F1 (0.35), suggesting significant confusion between pure layers and mixed layers.

### 2. Generalization Gap
* **Training vs. Testing:** The drop from **89% CV Accuracy** to **74% Test Accuracy** indicates some degree of overfitting to the training distribution, or that the test set contains geological variances not fully captured in the training data.

---

## Artifacts in this Folder

### `classification_report.txt`
The raw text output containing Precision, Recall, and F1-Scores for all 12 lithology classes.

### `confusion_matrix.png`

* **What to look for:** The diagonal line shows correct predictions.
* **Key Observation:** Note the heavy confusion between **Sandstone/Shale** and pure **Shale**, visible as off-diagonal hotspots.

### `training_history.png`

* **Left Plot (Loss):** Shows the Categorical Cross-Entropy loss decreasing over 50 epochs.
* **Right Plot (Accuracy):** Tracks the stability of the model during the 10-fold validation process.