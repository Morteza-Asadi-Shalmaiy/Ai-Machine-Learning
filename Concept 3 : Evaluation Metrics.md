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

**1. What is a Confusion Matrix, and why is it the foundation of all classification metrics?**

<details>
<summary>Answer</summary>

A confusion matrix is a 2x2 table that compares the model's predictions to the actual ground truth. It contains exactly 4 numbers:

- **TP (True Positive):** Correctly predicted Positive.
- **TN (True Negative):** Correctly predicted Negative.
- **FP (False Positive):** Incorrectly predicted Positive (Type I error).
- **FN (False Negative):** Incorrectly predicted Negative (Type II error).

It is the foundation because **every single classification metric** (Accuracy, Precision, Recall, F1, Specificity, TPR, FPR) is derived mathematically from these 4 numbers. If you give an interviewer the matrix, you can calculate any metric they ask for on the spot.
</details>

---

**2. Why is Accuracy a misleading metric for imbalanced datasets? Provide a concrete example.**

<details>
<summary>Answer</summary>

Accuracy is misleading because it counts True Negatives (TNs) as "correct," which heavily favors the majority class. 

**Example:** A dataset has 1,000 transactions. 995 are normal (Negative) and 5 are fraudulent (Positive). A dumb model that predicts "Not Fraud" for everything gets: TP=0, FN=5, FP=0, TN=995. 

Accuracy = (0 + 995) / 1000 = **99.5%**. The model looks amazing, but it caught **zero** fraudsters, making it completely useless for the business.
</details>

---

**3. Explain Precision and Recall. Give a real-world scenario where Precision is more important than Recall, and one where Recall is more important.**

<details>
<summary>Answer</summary>

- **Precision** = TP / (TP + FP). It answers: *"When I say 'Yes', how often am I right?"* It penalizes False Positives.
- **Recall** = TP / (TP + FN). It answers: *"Of all the real 'Yes' items, how many did I catch?"* It penalizes False Negatives.

**Precision > Recall (FP is costly):** **Spam Filter**. Predicting a real email as "Spam" (FP) makes the user miss an important meeting. You only want to mark something as spam if you are very sure. 

**Recall > Precision (FN is costly):** **Cancer Screening**. Predicting a patient as "No Cancer" (FN) means they walk away with a deadly disease. You are willing to have many false alarms (FPs) if it means you catch every single real cancer case.
</details>

---

**4. What is the F1-Score? Why use the harmonic mean instead of a regular arithmetic average?**

<details>
<summary>Answer</summary>

The F1-Score is the harmonic mean of Precision and Recall: **2 * (P * R) / (P + R)**. 

It is used when you need a single number that balances both metrics, and both False Positives and False Negatives are equally bad.

We use the **harmonic mean** instead of a simple arithmetic average because the harmonic mean punishes extreme imbalances. 
For example, if Precision = 0.9 and Recall = 0.1:
- Arithmetic mean = 0.5 (looks okay).
- Harmonic mean (F1) = ~0.18 (shows the model is actually terrible because it has almost zero recall). 
F1 only gets a high score when **both** Precision and Recall are high.
</details>

---

**5. What is the difference between ROC-AUC and PR-AUC? Which one should you use for a fraud detection model (0.5% fraud rate) and why?**

<details>
<summary>Answer</summary>

- **ROC-AUC** plots True Positive Rate (Recall) against False Positive Rate (FPR). 
- **PR-AUC** plots Precision against Recall.

For fraud detection with a 0.5% fraud rate, you should use **PR-AUC**. 

**Why:** ROC-AUC uses FPR in its calculation, and FPR uses True Negatives (TN) in its denominator. Since there are 99.5% Negatives, even a bad model will have a very low FPR, making the ROC-AUC look optimistically high. 

PR-AUC completely ignores True Negatives. It focuses only on the model's performance on the rare Positive class (Precision and Recall). It is much more sensitive to catching fraudsters and will give a brutally honest score.
</details>

---

**6. What is the F2-Score and how does it differ from the F1-Score? When would you use it?**

<details>
<summary>Answer</summary>

The F-Beta score is a weighted harmonic mean of Precision and Recall. 

- **F1-Score** gives equal weight (1:1) to Precision and Recall.
- **F2-Score** weights Recall **twice as much** as Precision (2:1). 

You use the **F2-Score** when False Negatives are significantly more costly than False Positives. 

**Example:** Fraud detection, epidemic screening, or airport security. You would rather have 100 false alarms (low precision) than let 1 terrorist/bomb through (high recall). So you optimize for F2.
</details>

---

**7. You built two models for a rare disease prediction. Model A has an ROC-AUC of 0.95. Model B has an ROC-AUC of 0.92 but a PR-AUC of 0.85. Model A only has a PR-AUC of 0.60. Which model do you deploy and why?**

<details>
<summary>Answer</summary>

You deploy **Model B**. 

Since this is a rare disease, the data is heavily imbalanced. As we know, ROC-AUC is overly optimistic for imbalanced data. 

Model A looks great on ROC-AUC (0.95), but its PR-AUC is a terrible 0.60, meaning it's actually struggling to find the rare positive cases without flooding you with false alarms. 

Model B has a much stronger PR-AUC (0.85), proving it is actually better at ranking the rare positives higher. When dealing with rare events, **PR-AUC is the truth-teller**, and you should always prioritize it over ROC-AUC.
</details>

---

**8. What is Log Loss? Why is it useful for probabilistic models?**

<details>
<summary>Answer</summary>

Log Loss (Cross-Entropy) measures the accuracy of your model's *probabilities*, not just its final labels. 

It penalizes confident wrong predictions heavily. 
- If a model predicts "Fraud" with 99% confidence, but it's actually "Not Fraud", Log Loss skyrockets.
- If a model predicts "Fraud" with 51% confidence, and it's wrong, Log Loss is much smaller.

It is useful when the business decision depends on the **risk/probability**. For example, if you are calculating expected financial loss, you need accurate probabilities (0.7 means it should actually be fraud 70% of the time), not just a binary "Fraud / Not Fraud" label.
</details>

---

**9. Explain Micro vs Macro F1-Score in a multi-class problem (e.g., classifying images of cats, dogs, and birds). Which one would you use if the dataset has 90% cats, 5% dogs, and 5% birds?**

<details>
<summary>Answer</summary>

- **Macro F1:** Calculates the F1-score individually for each class (Cat, Dog, Bird) and then takes the **arithmetic average**. Every class gets equal weight (33.3%). 
- **Micro F1:** Aggregates all the TPs, FPs, and FNs from *all* classes globally into one giant pool, and calculates the F1 from that. The majority class (Cats) will dominate this score.

For the dataset with 90% Cats, 5% Dogs, and 5% Birds, you should use **Macro F1**. 

**Why:** Micro F1 would basically just tell you how well the model predicts cats. If the model predicts "Cat" for everything, Micro F1 would be 90%. Macro F1 forces the model to perform well on the rare classes (Dogs and Birds) to get a good score, which is what you actually care about.
</details>

---

**10. (The Ultimate Boss Question): You are tasked with building a model to approve credit cards. False positives (denying a good customer) cost the bank $100 in lost interest. False negatives (approving a fraudster) cost the bank $5,000. The data has 2% fraud. Walk me through your entire metric strategy from model comparison to final deployment.**

<details>
<summary>Answer</summary>

*(This is how you land the job. Walk them through step-by-step):*

1. **Model Comparison:** Because the data is imbalanced (2% fraud), I will **not** use Accuracy or ROC-AUC. I will compare candidate models using **PR-AUC**, because it focuses strictly on the positive (fraud) class and ignores the 98% normal transactions.

2. **Cost-Aware Metric:** Since a False Negative costs $5,000 and a False Positive costs $100, a FN is **50x more costly** than a FP. Therefore, I will primarily optimize for **Recall** (to catch fraudsters) but I will monitor Precision. I would use the **F2-Score** (which weights Recall twice as much) as my single-number target metric.

3. **Choosing the Cutoff (Threshold):** I won't just use 50%. I will plot a **Precision-Recall Curve**, look at the probabilities, and calculate the **Expected Cost** for every possible threshold: 
   *(Cost = FN_rate * 5000 + FP_rate * 100)*.
   I will choose the exact threshold that minimizes this total dollar cost for the business.

4. **Final Validation:** I will check the **Confusion Matrix** at that chosen threshold to show the exact number of fraudsters caught, good customers denied, and fraudsters missed. This gives the business a clear, tangible picture of what to expect in production.
</details>
