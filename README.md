## 📊 Dataset
The dataset used in this project is quite large and cannot be uploaded to GitHub due to size limitations.

You can download the dataset from the link below:
https://d3ilbtxij3aepc.cloudfront.net/projects/CDS-Capstone-Projects/PRCP-1012-GameWinnerPred.zip

After downloading, extract the zip file and place the dataset in the project folder before running the notebook. 

# 🎮 Game Winner Prediction

A machine learning project to predict a player's winning percentage (`winPlacePerc`) in PUBG matches using player-level gameplay statistics.

---

## 📌 Project Overview

This project analyzes a large PUBG dataset with 4.4 million+ rows and 29 features. The goal is to understand what factors influence a player's chance of winning and build regression models to predict their final placement.

---

## 📂 Dataset

- **Source:** PUBG Match Stats (pubg.csv)
- **Rows:** 4.4 million+
- **Target Variable:** `winPlacePerc` (0 = last place, 1 = winner)
- **Features include:** kills, damage dealt, walk distance, heals, boosts, match type, and more

---

## 🔍 Project Workflow

1. **Exploratory Data Analysis (EDA)**
   - Univariate, Bivariate, and Multivariate analysis
   - Key insight: Walk distance is the strongest predictor of winning

2. **Data Preprocessing**
   - Removed duplicate and null rows
   - Handled outliers using IQR method and manual thresholds
   - Dropped irrelevant/redundant columns (Id, rankPoints, winPoints, etc.)

3. **Feature Engineering**
   - `totalDistance` = walkDistance + rideDistance + swimDistance
   - `headshotRatio` = headshotKills / kills
   - `aggressionIndex` = (kills + DBNOs) / matchDuration
   - `damagePerKill` = damageDealt / kills
   - `teamContribution` = assists + revives

4. **Encoding & Scaling**
   - Label Encoding for `matchType`
   - MinMax Scaling on continuous features

5. **Feature Importance Analysis**
   - Used LightGBM and XGBoost to identify low-importance features and drop them

6. **Model Training & Evaluation**
   - Trained 5 models: Linear Regression, Random Forest, XGBoost, LightGBM, MLP

---

## 📊 Model Results

| Model             | R² Train | R² Test | MAE  | RMSE |
|------------------|----------|---------|------|------|
| Linear Regression | 0.83     | 0.83    | 0.09 | 0.13 |
| Random Forest     | 0.99     | 0.93    | ~0.06| ~0.08|
| XGBoost           | 0.93     | 0.93    | 0.06 | 0.08 |
| LightGBM          | 0.93     | 0.93    | 0.06 | 0.08 |
| MLP               | 0.89     | 0.89    | —    | —    |

✅ **Best Models:** XGBoost and LightGBM — best balance of accuracy and generalization

---

## 🛠️ Libraries Used

- `pandas`, `numpy` — data handling
- `matplotlib`, `seaborn` — visualization
- `scikit-learn` — preprocessing and model evaluation
- `xgboost` — XGBoost model
- `lightgbm` — LightGBM model

---

## ⚠️ Challenges Faced

- Dataset had 4.4M+ rows — heavy on memory and computation
- Many columns had mostly zero values (kills, headshots, swim distance)
- Extreme outliers in rideDistance, weapons acquired, and kills
- Outdated ranking columns (killPoints, winPoints) had to be removed
- 16 different match types made comparison complex


