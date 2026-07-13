# Concept 3 : Evaluation Metrics

---
## Confusion Matrix for `Fraud` & `Not Fraud`
- Actually Positive (it IS fraud)
- Actually Negative (it is NOT fraud)
  
Our model says "Yes" or "No". Here are the 4 boxes/possiblities :

| | Model Predicts: YES (Positive) | Model Predicts: NO (Negative) |
| :--- | :--- | :--- |
| **Actually YES** | **TP** (True Positive) <br>*Correctly caught the fraud* | **FN** (False Negative) <br>*Missed the fraud (BAD)* |
| **Actually NO** | **FP** (False Positive) <br>*False alarm (wasted time)* | **TN** (True Negative) <br>*Correctly said it was fine* |

---

## Classification Metrics

| Metric | Formula | Plain English (The Vibe) | The Golden Rule (When to use it) |
| :--- | :--- | :--- | :--- |
| **Accuracy** | **(TP + TN) / Total** | "How many did I get totally right, period?" | **USE:** Only when classes are perfectly balanced (50% / 50%). <br> **AVOID:** If data is imbalanced (it lies). |
| **Precision** | **TP / (TP + FP)** | "When I say 'YES', how often am I right?" | **USE:** When **False Positives** are costly. <br> *(e.g., Spam filter, recommending bad products)* |
| **Recall** <br> *(aka TPR / Sensitivity)* | **TP / (TP + FN)** | "Of all the real 'YES' items, how many did I catch?" | **USE:** When **False Negatives** are costly. <br> *(e.g., Fraud, Cancer screening)* |
| **F1-Score** | **2 * (P * R) / (P + R)** <br> *(Harmonic Mean)* | "A balanced average of Precision and Recall." | **USE:** When FP and FN are **equally** bad, and you need one single number to pick a model. |
| **ROC-AUC** | Plots TPR (Recall) vs FPR across all thresholds. <br> (AUC = Area Under Curve) | "Regardless of my cutoff, does this model rank the positives higher than the negatives?" | **USE:** For balanced datasets, or when you just want to compare general ranking ability. <br> **AVOID:** On highly imbalanced data (it looks too optimistic). |



---
