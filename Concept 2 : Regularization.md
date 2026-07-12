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
- During training, you randomly "drop" (set to zero) a percentage of neurons in a layer for a single pass. (e.g., Dropout rate = 0.5 means half the neurons are turned off).
- Since any neuron can be turned off at any moment, the network cannot rely on a single "super neuron" or specific collaboration between neurons. It is forced to learn redundant, independent representations of the patterns so that if one pathway dies, another can take over.
- Exclusively for deep neural networks, especially when you have a massive amount of parameters and limited data. (Note: You turn it off during testing/prediction).

## Early Stopping
- During training, you monitor the validation loss after every epoch. The moment the validation loss stops decreasing and starts increasing (while training loss keeps dropping), you stop training immediately and roll back to the best checkpoint.
- Overfitting happens when the model spends too much time memorizing the noise in the training data. Early stopping cuts off the training process before it has time to do that.
- Almost always! It's the easiest regularization method because it costs nothing to implement and works with any model. Just remember to always keep a separate validation set to monitor.


---
