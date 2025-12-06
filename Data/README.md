# FORCE 2020 Dataset Information

## Overview

This project utilizes the **FORCE 2020 Lithology Challenge** dataset, which consists of well logs from the North Sea. The goal is to predict the lithology (rock type) from well log measurements (Gamma Ray, Resistivity, Density, etc.).

## Folder Contents

### 1. Field Information (`/Field info`)

This folder contains auxiliary metadata provided by the competition organizers:

* **`lithology scoring matrix cost function.xlsx`**: Defines the penalty matrix for misclassification (used to evaluate model performance).
* **`NPD_Lithostratigraphy_...xlsx`**: Information on geological groups and formations.
* **`Well logs abbreviation description.xlsx`**: Dictionary explaining the feature column names (e.g., `GR` = Gamma Ray).

### 2. Raw Data Files (Ignored via .gitignore)

The following files are part of the workflow but are **not uploaded** to this repository due to GitHub's 100MB file size limit and bandwidth constraints:

* `train.csv`: The main training dataset (approx. 1.2M rows).
* `test_features.csv`: Predictor variables for the test set.
* `test_target.csv`: True labels for the test set.

## How to Access the Data

**You do not need to download these files manually.**
The notebooks in this repository are configured to automatically load the dataset from a stable remote source (GitHub user content) during execution.

**Code Snippet (from `01_EDA.ipynb`):**

```python
# Data is loaded directly from the remote source to ensure reproducibility
train = pd.read_csv('[https://media.githubusercontent.com/.../train.csv](https://media.githubusercontent.com/.../train.csv)', sep=';')
