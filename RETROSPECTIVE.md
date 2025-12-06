# Capstone Retrospective: Lithological Classification of Geophysical well logs with Deep Learning

**Student Name:** Hussaini Ahmed  
**Cohort:** MIT Emerging Talent - Cohort 6  
**Project Track:** Track 2 (Capstone Project)  
**Date:** December 2025  

---

## 1. Executive Summary
This project aimed to automate the interpretation of subsurface well logs using the **FORCE 2020** dataset. By transitioning from traditional XGBoost methods to a **Deep Learning (ANN)** approach, I investigated whether neural networks could handle the noise and complexity of geological data. The final model successfully classifies 12 distinct lithology types, offering a scalable solution for reservoir characterization.

---

## 2. Technical Challenges & Solutions

### Challenge A: Severe Class Imbalance
**The Problem:** The dataset is heavily skewed towards common rocks like Shale (60%+) and Sandstone, while critical resources like Coal and Limestone represent less than 1% of the data. Initial models achieved high accuracy by simply guessing "Shale," which is a failure in a real-world context.

**The Solution:**  I moved beyond "Accuracy" as a metric and focused on **Weighted F1-Score** and the **Confusion Matrix**.
* I implemented robust data preprocessing (Standard Scaling) to ensure rare classes weren't drowned out by the magnitude of other features.

### Challenge B: Managing Large-Scale Data in Version Control
**The Problem:** The raw training data exceeded 150MB, hitting GitHub’s hard file limits and threatening the repository's bandwidth quota (LFS).

**The Solution:** * Instead of bloating the repository, I architected a **Remote Data Loading** pipeline. 
* The notebooks now fetch data directly from a stable external URL (`media.githubusercontent.com`) via Pandas. 
* **Result:** A reproducible, lightweight (<5MB) repository that adheres to open-source best practices.

---

## 3. Reflection: "If I Could Start Over"
If I were to reboot this project with my current knowledge, I would introduce these architectural changes:

1.  **Sequential Modeling (RNNs/LSTMs):** * *Why?* Well logs are depth-dependent sequences. A standard ANN treats every row as independent, ignoring the geological context of the rock layers above and below. An LSTM would capture these spatial dependencies.
2.  **Advanced Imputation:**
    * *Why?* I used Mean Imputation for missing logs. In the future, I would use a multivariate regression approach (like `IterativeImputer`) to predict missing log values based on correlations with other existing logs.

---

## 4. Professional Growth
This Capstone bridged the gap between theoretical coursework and production-level Machine Learning:
* **End-to-End Workflow:** I now feel confident managing the full lifecycle: *Data Engineering $\rightarrow$ Model Architecture $\rightarrow$ Evaluation $\rightarrow$ Documentation*.
* **Domain Adaptation:** It taught me how to translate domain-specific constraints (Geology) into mathematical constraints (Cost Functions/Loss Matrices).

---

## 5. Milestone Deliverables (CDSP Framework)

| Milestone | Deliverable Status | Key Artifact |
| :--- | :--- | :--- |
| **M0** | ✅ Complete | Project Board & `.gitignore` setup |
| **M1** | ✅ Complete | Problem Statement in `README.md` |
| **M2** | ✅ Complete | Data Pipeline in `01_EDA.ipynb` |
| **M3** | ✅ Complete | ANN Model & Classification Report in `02_ANN.ipynb` |
| **M4** | ✅ Complete | Public-facing Summary in `Presentation/` |
| **M5** | ✅ Complete | Final Slide Deck |

---

## 6. Final Thoughts
This project was a rigorous exercise in balancing model complexity with data reality. While Deep Learning offers power, it requires discipline in data handling. I am proud to submit a repository that is not just a "model," but a reproducible scientific workflow.