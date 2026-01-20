# CS:GO Round Winner Prediction | Machine Learning Pipeline

This project implements an end-to-end Machine Learning Pipeline to predict the winner of a Counter-Strike: Global Offensive (CS:GO) round (Counter-Terrorists vs. Terrorists).

The goal was to build a robust, production-ready pipeline that prevents data leakage and ensures reproducibility using industry best practices.

*Note: This project was developed as part of an advanced Machine Learning academic module, simulating a real-world technical assessment scenario.*

## Project Overview

The dataset consists of **122,410 round snapshots** extracted from over **700 high-level professional matches**.
Each row represents a specific moment in a round, containing **94 features** such as:

*   **Economy:** Team money, equipment value, spend.
*   **Status:** Health points, armor, helmets.
*   **Loadout:** Specific weapons, grenades (flashbangs, smokes), and defuse kits.
*   **Map:** The map being played (e.g., Dust2, Inferno).

## Methodology & Tech Stack

I approached this as a Data Engineering and Data Science problem, focusing on modularity.

*   **Language:** Python
*   **Data Processing:** Pandas, NumPy
*   **Visualization:** Matplotlib, Seaborn
*   **Machine Learning:** Scikit-Learn, XGBoost

### Key Steps:

1.  **Exploratory Data Analysis (EDA):** Identified class balance (CT vs T) and feature correlations.
2.  **Data Cleaning & Encoding:** Handled categorical variables (Map) and target encoding.
3.  **Strict Train/Test Split:** Performed the split **before** any normalization to prevent **Data Leakage**.
4.  **Pipeline Construction:**
    *   **Feature Selection:** Used `SelectKBest` (ANOVA) to reduce dimensionality from 94 to the top 20-30 impactful features.
    *   **Normalization:** Applied `StandardScaler` to handle varying scales (e.g., Money vs. Health).
5.  **Model Benchmarking:** Compared **Random Forest** vs. **XGBoost**.
6.  **Hyperparameter Tuning:** Utilized `RandomizedSearchCV` to optimize estimators and tree depth.

## Results

After optimization, the **Random Forest** model achieved the best performance, proving that complex ensemble methods (like XGBoost) are not always superior for every dataset.

| Metric | Result (Test Set) |
| :--- | :--- |
| **Accuracy** | **83.75%** |
| **F1-Score** | **0.8375** |
| **ROC-AUC** | **0.9221** |

**Key Insight:** The model identified that **Team Money** and **Armor/Helmets** variables were often more predictive of a round win than the specific weapons used.

## How to Run

1. **Download the Dataset:**
   The dataset file is too large for GitHub. Please download it from the source:
   [Download csgo_round_snapshots.xlsx](https://static.plataforma.grupoa.education/pucpr/111/7ff2afe1-81b8-4b8d-b15a-a77e5b0bc141.zip)
   *Extract the zip and place `csgo_round_snapshots.xlsx` in the root folder.*

2. Clone this repository:
   ```bash
   git clone https://github.com/Matheus432hz/csgo-round-prediction.git

3. Install requirements:
   ```bash
   pip install pandas scikit-learn xgboost matplotlib seaborn openpyxl

4. Run the jupyter Notebook:
   ```bash
   jupyter notebook csgo_prediction_pipeline.ipynb
