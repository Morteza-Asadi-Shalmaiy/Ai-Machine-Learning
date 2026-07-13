# Concept 2 : Regularization
It is a solution for high variance (overfitting), Sacrifice training performance to improve test performance

---

## L1 (Lasso)
- Adds `λ * Σ|weight|` to the loss function.
- It penalizes large weights linearly. Because of the absolute value shape, it has a unique effect : it pushes less-important weights all the way to exactly zero. This completely removes those features from the model.
- Use this when you suspect that most of your features are completely irrelevant. It acts as automatic feature selection and gives you a simpler, faster model

## L2 (Ridge)
- Adds `λ * Σ(weight²)` to the loss function.
- It penalizes large weights quadratically. To minimize the loss, the model shrinks all weights toward zero, but it never makes them exactly zero. It spreads the "punishment" evenly across all features.
- Use this as your default when you believe most of your features have at least a little bit of predictive power. It also works great when you have correlated features (multicollinearity)

## Dropout (Neural Networks only)
- It prevents co-adaptation of neurons.
- During training, you randomly "drop" (set to zero) a percentage of neurons in a layer for a single pass. (e.g., Dropout rate = 0.5 means half the neurons are turned off).
- Since any neuron can be turned off at any moment, the network cannot rely on a single "super neuron" or specific collaboration between neurons. It is forced to learn redundant, independent representations of the patterns so that if one pathway dies, another can take over.
- Exclusively for deep neural networks, especially when you have a massive amount of parameters and limited data. (Note: You turn it off during testing/prediction).

## Early Stopping
- During training, you monitor the validation loss after every epoch. The moment the validation loss stops decreasing and starts increasing (while training loss keeps dropping), you stop training immediately and roll back to the best checkpoint.
- Overfitting happens when the model spends too much time memorizing the noise in the training data. Early stopping cuts off the training process before it has time to do that.
- Almost always! It's the easiest regularization method because it costs nothing to implement and works with any model. Just remember to always keep a separate validation set to monitor.

---

**1. What is regularization and why do we use it?**

<details>
<summary>Answer</summary>

- **What it is:** A set of techniques that add a penalty to your model to constrain its complexity.
- **Why we use it:** To fight **overfitting (high variance)**. It forces the model to generalize better to unseen data by trading a bit of training accuracy for better test accuracy.
</details>

---

**2. What is the difference between L1 (Lasso) and L2 (Ridge) regularization?**

<details>
<summary>Answer</summary>

- **L1 (Lasso):** Adds `λ * Σ|weight|` to the loss. It shrinks weights to **exactly zero**, acting as built-in **feature selection**.
- **L2 (Ridge):** Adds `λ * Σ(weight²)` to the loss. It shrinks weights **close to zero, but never exactly zero**, keeping all features but reducing their impact.
- **When to use:** Use L1 when you suspect many features are irrelevant. Use L2 as your default when most features matter a little bit.
</details>

---

**3. How does increasing λ (lambda) affect bias and variance in L2 regularization?**

<details>
<summary>Answer</summary>

- **Bias increases** – The model becomes less flexible and can't capture complex patterns.
- **Variance decreases** – The model is less sensitive to noise in the training data.
- **Why:** As λ grows very large, weights are forced toward zero. The model becomes almost flat (like a horizontal line), which is simple but may underfit.
</details>

---

**4. What is Dropout and how does it prevent overfitting?**

<details>
<summary>Answer</summary>

- **What it is:** A regularization technique for neural networks that randomly turns off a percentage of neurons during each training pass.
- **How it prevents overfitting:** It prevents **co-adaptation** – neurons can't rely on specific other neurons to be there. This forces the network to learn **redundant, independent features** so that if one pathway dies, another can take over.
- **Note:** Dropout is **only** for neural networks. You turn it off during testing.
</details>

---

**5. What is Early Stopping and how does it work?**

<details>
<summary>Answer</summary>

- **What it is:** Monitoring validation loss during training and stopping the moment it starts increasing, even if training loss keeps dropping.
- **How it works:** Overfitting happens when the model spends too much time memorizing noise. Early stopping cuts training short **before** it has time to do that.
- **Why it's great:** It's free – costs nothing to implement and works with any model.
</details>

---

**6. Can you use Dropout on a Random Forest or Linear Regression?**

<details>
<summary>Answer</summary>

- **No.** Dropout specifically targets the **co-adaptation of neurons in hidden layers** of neural networks.
- Tree-based models (Random Forest, XGBoost) and linear models don't have neurons or interconnected pathways, so Dropout doesn't apply to them.
- For those models, I'd use L1, L2, or Early Stopping instead.
</details>

---

**7. Why does L1 push weights to zero but L2 doesn't?**

<details>
<summary>Answer</summary>

- **L1** uses the absolute value `|weight|`. The derivative is constant (±1), so it applies the same pressure regardless of how small the weight gets, pushing it all the way to zero.
- **L2** uses `weight²`. The derivative is `2*weight` – as the weight gets smaller, the penalty gets weaker. So it shrinks weights close to zero but never eliminates them completely.
- **Simple analogy:** L1 pushes everything toward zero evenly. L2 gently nudges big weights down but barely touches tiny ones.
</details>

---

**8. What's the difference between bias and variance?**

<details>
<summary>Answer</summary>

- **Bias:** Error from incorrect assumptions. High bias = model is too simple (underfitting). Example: using a straight line for a curved pattern.
- **Variance:** Error from sensitivity to training data. High variance = model is too complex (overfitting). Example: a wiggly line that perfectly fits every training point but fails on new data.
- **Trade-off:** You can't eliminate both – reducing one usually increases the other.
</details>

---

**9. How do you know if your model is overfitting?**

<details>
<summary>Answer</summary>

- **Signs:** Great performance on training data, but poor performance on validation/test data.
- **The gap:** If training accuracy is 99% and validation is 70%, that's a classic sign of overfitting.
- **Fixes:** Add regularization (L1, L2, Dropout), simplify the model, get more data, or use Early Stopping.
</details>

---

**10. Which regularization technique should I choose and why?**

<details>
<summary>Answer</summary>

- **L2 (Ridge):** Default choice. Use when most features are at least somewhat useful.
- **L1 (Lasso):** Use when I suspect most features are useless and I want feature selection.
- **Dropout:** Use for neural networks, especially with limited data.
- **Early Stopping:** Use **always** – it's free and works alongside any other method.
</details>

---

**🔥 Final Interview Tip:** If they ask you a broad question like *"How would you handle overfitting?"*, just run down this list:

> *"First, I'd simplify the model. Then I'd add L2 regularization to constrain weights, or L1 if I want feature selection. If it's a neural net, I'd add Dropout. And I'd always use Early Stopping to monitor validation loss."*

You're ready! Want me to make you a quick **comparison table** summary for last-minute review?
