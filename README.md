# Lithological Classification of Geophysical Well Logs using Deep Learning
### MIT Emerging Talent - ELO2 Capstone Project

**Author:** Hussaini Ahmed  
**Program:** MIT Emerging Talent, Cohort 6 (Certificate in Computer and Data Science)  
**Status:** Complete

---

## Project Overview
In the energy and carbon storage industries, accurately identifying rock types (lithology) from subsurface well logs is critical for reservoir characterization. Traditionally, this is performed by human interpreters—a process that is time-consuming, subjective, and prone to error.

This project automates lithofacies classification using the **FORCE 2020** dataset. By implementing a **Deep Feed-Forward Neural Network (ANN)**, this project addresses high-dimensional subsurface data challenges, including extreme class imbalance and missing sensor readings.

### Research Objectives
1. **Feasibility:** Can a Feed-Forward Neural Network (MLP) accurately classify complex lithofacies compared to traditional interpretation?
2. **Stability:** How do preprocessing techniques (Mean Imputation and Standardization) affect model stability given the sparsity of well logs?
3. **Imbalance:** How effectively can the model handle a **7000:1** class imbalance ratio between Shale and rare formations like Basement rocks?

---

## Dataset: FORCE 2020
The dataset consists of **1.17 million** training samples from 98 wells in the North Sea.

*   **Target:** 12 Lithology Classes (Shale, Sandstone, Limestone, etc.)
*   **Features:** 29 initial features including depth-indexed wireline logs (Gamma Ray, Resistivity, Density, Neutron Porosity) and spatial coordinates.
*   **Key Challenges Identified (EDA):**
    *   **Class Imbalance:** Shale constitutes **61.6%** of the data, while Basement rocks constitute **0.01%**.
    *   **Missing Data:** Logs like SGR (Spectral Gamma Ray) and RXO are missing in >70% of samples.

---

## Methodology

### 1. Data Cleaning & Preprocessing
*   **Sparse Feature Removal:** Dropped columns with >50% missingness (SGR, ROPA, RXO, DCAL) to reduce noise.
*   **Imputation:** Applied **Mean Imputation** to handle remaining NaNs (essential for Neural Networks, unlike Tree-based models).
*   **Scaling:** Standardized all input features (Mean=0, Std=1) for stable gradient descent.

### 2. Feature Engineering
To capture the vertical geological trends inherent in well logs, we implemented **Vectorized Spatial Windowing**:
*   **Petrophysical Ratios:** Calculated `GR/RHOB` and `NPHI - Density` porosity differences.
*   **Lag/Lead Features:** Created input vectors incorporating data from depths immediately above and below the target depth.
*   **Gradients:** Calculated depth-based derivatives to capture lithological transitions.

### 3. Model Architecture (ANN)
A Multi-Layer Perceptron (MLP) built with **TensorFlow/Keras**:
*   **Input Layer:** 26 standardized features.
*   **Hidden Layers:** 3 Dense Layers (256 $\to$ 128 $\to$ 64 neurons) with ReLU activation.
*   **Regularization:** Batch Normalization and Dropout (0.3) applied after every hidden layer to prevent overfitting.
*   **Output:** Softmax activation for 12-class probability distribution.

---

## Key Results & Findings

The model was evaluated on a blind test set of **137,000 samples**.

| Metric | Score | Notes |
| :--- | :--- | :--- |
| **Cross-Validation Accuracy** | **89.36%** | Stable across 10 folds. |
| **Test Accuracy** | **74.00%** | Generalization gap observed. |
| **Weighted F1-Score** | **0.73** | High performance on dominant classes (Shale/Sandstone). |
| **Macro F1-Score** | **0.37** | Struggles with minority classes (Chalk, Dolomite). |

*   **Successes:** The model achieves high precision (0.84) and recall (0.85) for the dominant **Shale** class.
*   **Limitations:** The "Limestone" and "Chalk" classes overlap significantly in feature space, leading to misclassification. The extreme class imbalance remains the primary bottleneck for rare lithologies.

---

## Repository Structure

```
├── 📁Data/                      # Dataset & Documentation
│   ├── 📁Field info/            # Domain knowledge & Mapping files
│   │   ├── lithology scoring matrix cost function.xlsx
│   │   ├── NPD_Lithostratigraphy_groups_all_wells.xlsx
│   │   └── Well logs abbreviation description.xlsx
│   ├── train.csv                # Training Data (1.17M samples)
│   ├── test_features.csv        # Blind Test Features
│   ├── test_target.csv          # Blind Test Labels
│   ├── hidden_test.csv          # Validation Set
│   └── README.md                # Data dictionary and usage notes
├── 📁Notebooks/                 # Computational Narrative
│   ├── 01_EDA.ipynb             # Exploratory Analysis (Data Cleaning, Viz)
│   └── 02_ANN_Model.ipynb       # Feature Engineering & ANN Implementation
├── 📁Presentation/              # Milestone 5 Deliverable
│   └── presentation.pdf         # Technical slide deck (2.5 min summary)
├── 📁Results/                   # Milestone 4 Artifacts
│   ├── classification_report.txt
│   ├── confusion_matrix.png
│   ├── training_history.png
│   └── README.md                # Analysis of results
├── .gitignore                   # Git configuration
├── README.md                    # Project landing page (This file)
├── requirements.txt             # Python dependencies
└── RETROSPECTIVE.md             # ELO2 Final Reflection
```

Usage
1. Clone the repository:
2. Install dependencies:
3. Run the Analysis: Open Notebooks/01_EDA.ipynb to view the data distribution and Notebooks/02_ANN_Model.ipynb to train the Neural Network.

| Milestone         | Deliverable                                      | Status      |
|-------------------|--------------------------------------------------|-------------|
| 1. Problem ID     | Research Questions defined                       | ✅ Completed |
| 2. Data Collection| FORCE 2020 Data cleaned & hosted                 | ✅ Completed |
| 3. Data Analysis  | EDA & Deep Learning Model trained                | ✅ Completed |
| 4. Communication  | Visualization Artifacts (Results/)               | ✅ Completed |
| 5. Presentation   | Final Slide Deck (Presentation/)                 | ✅ Completed |
| Reflection        | Retrospective (RETROSPECTIVE.md)                 | ✅ Completed |

--------------------------------------------------------------------------------

## Data Source

Lithofacies data used in this project was provided by the FORCE Machine Learning competition with well logs and seismic data (Bormann et al., 2020).

**Citation:**
Bormann P., Aursand P., Dilib F., Dischington P., Manral S. 2020. 2020 FORCE Machine Learning Contest.

--------------------------------------------------------------------------------