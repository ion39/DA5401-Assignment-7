# **DA5401 A7: Multi-Class Model Selection using ROC and Precision-Recall Curves**

# Name : Pragati L
# Roll No: CE22B089

## **Objective**

Select the best multi-class classifier for the **Landsat Satellite Dataset** using **ROC** and **Precision-Recall Curves (PRC)**. Focus on threshold-independent metrics rather than accuracy alone.


## **Problem Statement**

* Classify land-cover types from the **UCI Landsat Satellite Dataset** (6 classes).
* Challenge: High-dimensional features with potential class overlap.
* Approach: Train multiple models and evaluate using **One-vs-Rest (OvR) ROC and PRC**.


## **Data Preparation**

1. Run !pip install ucimlrepo to install the repo 
2. Load and standardize features.
3. Train/test split (e.g., 80/20).
4. Train models on training data.
5. Baseline evaluation: compute **Accuracy** and **Weighted F1-Score**.


## **ROC Analysis**

* **One-vs-Rest (OvR) Approach:**
  Treat each class as positive vs all others, compute **ROC curve and AUC** per class.
* **Macro-Average ROC:** Average AUCs across all classes.


$$\text{TPR} = \frac{TP}{TP + FN}, \quad \text{FPR} = \frac{FP}{FP + TN}$$


* **Observation:** Highest Macro-AUC identifies the best model; AUC < 0.5 indicates systematic misclassification or poor discrimination.


## **Precision-Recall Curve (PRC) Analysis**

* PRC is more sensitive to **class imbalance**, focusing on **positive prediction quality**.


$$\text{Precision} = \frac{TP}{TP + FP}, \quad \text{Recall} = \frac{TP}{TP + FN}$$


* **Macro-Average PRC:** Average precision-recall across all classes.
* Models with low AP drop sharply as recall increases, indicating poor precision.


## **Synthesis**

* Top and bottom models (e.g., KNN/SVM vs Dummy) are consistent across **F1, ROC-AUC, and PRC-AP**.
* Mid-tier models may show minor rank differences:

  * **ROC-AUC:** Measures ranking quality, insensitive to false positives.
  * **PRC-AP:** Sensitive to false positives; penalizes poor precision at high recall.


## **Recommendation**

* **Best Model:** **KNN**

  * Highest Macro-AUC and Macro-AP.
  * Excellent precision-recall balance across thresholds.
  * Non-parametric, captures non-linear relationships in features.

* **Alternative:** **SVM**

  * Similar ROC-AUC, slightly lower PRC-AP.
  * Scalable for high-dimensional data.

* **Not Recommended:** **Dummy**

  * AUC ≈ 0.5, AP ≈ 0.17; performs near chance.


## **Brownie Points**

* **RandomForest & XGBoost:** Competitive tree-based models, often near KNN/SVM.
* **Low-AUC Model:** Perceptron or poorly tuned linear models produced AUC < 0.5, failing to separate classes effectively.


## **Conclusion**

KNN is the optimal choice for multi-class land-cover classification with Landsat data. ROC-AUC ensures reliable ranking, while PRC-AP ensures high-quality positive predictions. Threshold-independent metrics provide robust model comparison beyond accuracy.

