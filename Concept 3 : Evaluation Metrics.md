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
