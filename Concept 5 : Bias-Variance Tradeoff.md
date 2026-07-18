# Concept 5 : Train/Val/Test Methodology, Cross-Validation, Data Leakage


**Practice question:**
> A colleague preprocesses the entire dataset (imputing missing values, scaling features) *before* doing the train/test split. What's wrong with this, and how would you fix the pipeline?

---

**Train Set (Homework) :**
- You use this to learn the formulas. The model sees this data and updates its internal "brain" (parameters) to get better at solving these problems.  

**Validation Set (Practice Quizzes) :**
- After doing homework, you take a few practice tests. You check your score, realize you're weak in geometry, and decide to study more geometry (this is **tuning hyperparameters**). You can look at this data multiple times to adjust your study strategy.  

**Test Set (Final Exam) :**
- You have **never** seen these questions. You take it *once* at the very end. This is your true grade—it tells you if you actually learned the material or just memorized the homework answers.

**What is Cross-Validation (k-fold)?**  
- Instead of taking just *one* practice quiz, you split your homework into 5 chunks. You study on 4 chunks, quiz yourself on the 1 leftover, and rotate through all 5. This gives you 5 practice scores instead of 1—much more reliable for judging your true ability, especially when you don't have much homework data. Reduces variance in your performance estimate vs a single train/val split — useful with limited data.

**Data leakage:** 
- when information from outside the training set (often from the future, or from the target itself) sneaks into training, giving unrealistically good results that collapse in production. Classic examples: scaling/normalizing using statistics computed on the *full* dataset (including test data) before splitting; including a feature that's a proxy for the target (e.g., "days until diagnosis" when predicting diagnosis).

---
