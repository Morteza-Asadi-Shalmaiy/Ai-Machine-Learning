## 🧠 Concept Teaching

### 1. Default arguments
```python
def train(model, lr=0.001, epochs=10):
    ...
```
- Default values are evaluated **once** when the function is defined, not each call.  
- **Never** use mutable defaults like `def f(lst=[])` — it creates a single shared list across calls. Use `None` and set inside instead.  
- ML relevance: hyperparameters, model configs, convenience wrappers.

### 2. `*args` and `**kwargs`
- `*args` collects **extra positional arguments** into a tuple.
- `**kwargs` collects **extra keyword arguments** into a dictionary.
- They let you write functions that accept an arbitrary number of inputs.  
- `**kwargs` is ubiquitous for passing flexible configuration dicts or forwarding arguments to another function (e.g., `model(**hyperparams)`, `DataLoader(**loader_args)`).  
- ML relevance: building dataset configs, wrapping training loops that take arbitrary parameters, passing through model settings.

### 3. Lambdas
- Anonymous one‑line function: `lambda x: x['accuracy']`.
- Commonly used as the `key` argument in `sorted()`, `max()`, etc.  
- Also used in `map()` and `filter()`, but prefer list comprehensions when the logic gets longer.  
- ML relevance: sorting experiment results by a metric, quickly extracting a value from a list of dicts.

---

## 🧪 Your Exercise (Multi‑part)

You're building a small utility to manage **ML experiment results**. Write the following functions in pure Python (no external libs needed). Test each part with a few examples in your head or code.

### Part 1 – `create_experiment(name, **kwargs)`
Return a dict with key `'name'` and all other keys/values from `kwargs`.  
```python
>>> create_experiment('exp1', lr=0.01, epochs=10, batch_size=32)
{'name': 'exp1', 'lr': 0.01, 'epochs': 10, 'batch_size': 32}
```

### Part 2 – `sort_experiments(experiments, by, reverse=True)`
`experiments` is a list of dicts like those from Part 1.  
Use `sorted()` with a **lambda** to sort by the given key `by`. The `reverse` parameter should be `True` by default (so highest first).  
```python
exps = [
    {'name': 'A', 'accuracy': 0.92},
    {'name': 'B', 'accuracy': 0.87},
    {'name': 'C', 'accuracy': 0.95}
]
>>> sort_experiments(exps, 'accuracy')
[{'name': 'C', 'accuracy': 0.95}, {'name': 'A', 'accuracy': 0.92}, {'name': 'B', 'accuracy': 0.87}]
```

### Part 3 – `top_experiments(experiments, metric, n=3)`
Return the top `n` experiments by `metric`.  
- Reuse `sort_experiments` inside (or write your own lambda directly), using a default argument for `n`.  
- Handle the case where a dictionary is **missing** the metric gracefully: skip it (don’t crash), and optionally print a warning.  
```python
# If 'C' is missing 'accuracy', top 2 should still work.
```

### Part 4 – `aggregate_metrics(*metrics)`
Accept any number of numeric metric values (floats/ints) via `*args`. Return a dict with `'mean'`, `'min'`, `'max'`.  
```python
>>> aggregate_metrics(0.92, 0.87, 0.95)
{'mean': 0.91333..., 'min': 0.87, 'max': 0.95}
```

---

## 🎯 Ready?
Write all four functions (plus any helper code you need) in a single reply. I’ll grade it on correctness, edge cases, style, and how you handle the tricky bits (missing keys, mutable defaults if they appear, using the right idioms). No pseudocode—real executable Python. Go!
