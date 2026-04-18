# 🧠 Parkinson's Disease Classification using Machine Learning 

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-ML-orange.svg)
![Status](https://img.shields.io/badge/Status-Completed-success.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

---

## 📌 Overview

This project builds a machine learning model to classify whether a patient has Parkinson’s Disease (PD) based on voice/speech features.

The dataset contains biomedical voice measurements extracted from speech recordings. The goal is to predict the target variable:

- `0` → Healthy  
- `1` → Parkinson’s Disease  

---

## ⚠️ Problem Statement

The model is used in a sensitive medical scenario:

> Patients predicted as "sick" will receive a highly effective treatment,  
> but the treatment may cause severe harm if given to a healthy person.

This makes **false positives extremely dangerous**, and directly influences how the model is evaluated and optimized.

---

## 📊 Dataset

- Samples: 756  
- Features: 754 numerical features  
- Target: `class`  

### Key Characteristics:
- High-dimensional dataset  
- Slight class imbalance (more sick than healthy)  
- All features are numeric  

---

## ⚙️ Project Pipeline

### 1. Data Preprocessing
- Missing values handled using **median imputation**
- Features scaled using **StandardScaler**
- Pipeline ensures consistent transformations

### 2. Train/Test Split
- Performed using `train_test_split`
- Stratified split to preserve class distribution

### 3. Model Selection
- Model: **Logistic Regression**
- Regularization applied (`C = 1`) to reduce overfitting

### 4. Evaluation Metrics
- Accuracy  
- Precision  
- Recall  
- F1-score  
- Confusion Matrix  

---

## 📉 Overfitting Analysis

The model shows **clear overfitting**:

- Training accuracy: **100%**
- Test accuracy: **~82%**

### Reason:
- Very high number of features (~754)
- Number of features is close to number of samples (~756)
- Model can memorize training data instead of generalizing

### Conclusion:
The model fits training data perfectly but does not generalize well to unseen data.

---

## 🎯 Threshold Optimization

Instead of using the default threshold (0.5), multiple thresholds were explored.

### Why?

Because in this medical context:

- False Positive (healthy → predicted sick) = **very dangerous**
- False Negative (sick → predicted healthy) = less critical

---

### Strategy

We prioritize **Precision** over Recall.

- Precision answers:  
  *"When the model predicts sick, how often is it correct?"*

---

### Final Choice

- Selected threshold: **0.8**

### Results:

| Metric              | Value |
|--------------------|------|
| Precision (Sick)   | 0.90 |
| Recall (Sick)      | 0.86 |
| Accuracy           | 0.83 |

---

### Interpretation

- Higher precision reduces the risk of treating healthy patients incorrectly
- Slight decrease in recall is acceptable given the medical risk
- The model becomes more conservative in predicting "sick"

---

## 📈 Visualization

- Precision vs Recall vs Threshold plot  
- Confusion Matrix (raw and normalized)  

---

## 💡 Key Insights

- High-dimensional data increases risk of overfitting  
- Accuracy alone is not reliable in medical problems  
- Threshold tuning is critical in real-world applications  
- Precision is more important than recall in high-risk scenarios  

---

## ▶️ How to Run

```bash
# Clone the repository
git clone https://github.com/Maryam-SKaik/parkinsons-disease-classification.git

# Navigate into the project
cd parkinsons-disease-classification

# Open the notebook
jupyter notebook
```

---

## 📁 Project Structure

``` pgsql
parkinsons-disease-classification/
│
├── parkinsons_classification.ipynb
├── README.md
└── data/
    └── pd_speech_features.csv
```

---

## 👩‍💻 Author

**Maryam Skaik**

Computer Science Student | Backend Developer | ML Enthusiast

---

## 📄 License

This project is licensed under the MIT License.
