# Concept 5 : Train/Val/Test Methodology, Cross-Validation, Data Leakage

## 5. 

A favorite "gotcha" category — interviewers use this to check if you actually understand *why* the methodology exists, not just the steps.

- **Train set:** fit model parameters.
- **Validation set:** tune hyperparameters, model selection.
- **Test set:** final, untouched-until-the-end evaluation of generalization.
- **Cross-validation (k-fold):** split data into k folds, train on k-1, validate on the remaining fold, rotate. Reduces variance in your performance estimate vs a single train/val split — useful with limited data.
- **Data leakage:** when information from outside the training set (often from the future, or from the target itself) sneaks into training, giving unrealistically good results that collapse in production. Classic examples: scaling/normalizing using statistics computed on the *full* dataset (including test data) before splitting; including a feature that's a proxy for the target (e.g., "days until diagnosis" when predicting diagnosis).

**Practice question:**
> A colleague preprocesses the entire dataset (imputing missing values, scaling features) *before* doing the train/test split. What's wrong with this, and how would you fix the pipeline?

---
