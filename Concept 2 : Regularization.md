Concept 2 : Regularization
# Core ML Concepts — Interview Prep Study Guide

How to use this: read one concept, actually try to explain it out loud (or write it) before checking the "how interviewers test this" section. Then attempt the practice question yourself. When you come back to Claude, say something like "I studied Regularization, here's my answer to the practice question: ..." and you'll get evaluated and moved to the next concept.

Status: ✅ = covered together already. Everything else is what's left.

---

## 2. Regularization

Regularization fights **variance** — it constrains model complexity so the model can't overfit to training noise.

- **L2 (Ridge):** adds `λ * Σ(weights²)` to the loss. Shrinks weights smoothly toward zero, rarely exactly zero. Good default when you believe most features matter a little.
- **L1 (Lasso):** adds `λ * Σ|weights|` to the loss. Can push weights to exactly zero → built-in feature selection. Good when you suspect many features are irrelevant.
- **Dropout** (neural nets): randomly zeroes out neurons during training → prevents co-adaptation, forces redundant representations.
- **Early stopping:** stop training when validation loss starts rising, even if training loss keeps falling.

**Practice question:**
> You're using L2 regularization and increase λ (lambda) significantly. What happens to your model's bias and variance, and why?

*Think about: what happens to the weights as λ grows very large, and what that does to the model's effective complexity.*

---
