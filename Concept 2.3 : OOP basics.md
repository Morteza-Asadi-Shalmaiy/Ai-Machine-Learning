## Module 3: OOP Basics (classes, `__init__`, inheritance)

### Why this matters for AI Engineer interviews

Every PyTorch model you’ll ever write follows this exact pattern:

```python
class MyModel(nn.Module):
    def __init__(self):
        super().__init__()          # <-- inheritance
        self.linear = nn.Linear(10, 2)  # <-- attribute in __init__

    def forward(self, x):
        return self.linear(x)
```

If you don’t understand what `class`, `__init__`, `self`, and `super()` are doing, PyTorch will feel like voodoo. Interviewers will ask you to implement a tiny model from scratch (or a training loop that uses a class) specifically to see if you understand these mechanics, not just the ML math.

---

### Concept 1: Classes and objects

A **class** is a blueprint. An **object** is an instance of that blueprint.

```python
class Dog:
    def __init__(self, name):
        self.name = name

    def bark(self):
        print(f"{self.name} says woof")
```

- `__init__` is the **constructor** – it runs automatically when you create a new object.  
- `self` refers to the specific instance being created or operated on. It's how you attach data (`self.name`) and call methods (`self.bark()`).

```python
fido = Dog("Fido")
fido.bark()   # "Fido says woof"
```

In ML: `self.linear = nn.Linear(...)` is attaching a layer to the model instance. When you later call `model(x)`, it uses those layers.

---

### Concept 2: Inheritance

A class can inherit from another class, getting all its methods and attributes. This is how we build on existing code.

```python
class Animal:
    def __init__(self, species):
        self.species = species

class Cat(Animal):   # Cat inherits from Animal
    def __init__(self, name):
        super().__init__('cat')   # calls Animal's __init__
        self.name = name
```

- `class Cat(Animal):` says Cat is a kind of Animal.  
- `super().__init__(...)` calls the **parent** class’s `__init__`. This is crucial so the parent sets up its own internal state.  

In PyTorch, `nn.Module` is the parent class that knows how to track layers, parameters, and gradients. If you forget `super().__init__()`, your model will silently fail (parameters won't be registered). That’s a classic interview gotcha.

---

### Concept 3: `__init__` details and common pitfalls

- `self` must be the first parameter of every instance method, but you don’t pass it when calling – Python handles it.  
- Attributes can be added later, but it's cleanest to set them all in `__init__`.  
- Default arguments in `__init__` are allowed and common (e.g., `def __init__(self, lr=0.001)`).

---

### The Direct Link to `nn.Module`

```python
import torch.nn as nn

class SimpleClassifier(nn.Module):
    def __init__(self, input_dim, hidden_dim, output_dim):
        super().__init__()                        # registers module
        self.fc1 = nn.Linear(input_dim, hidden_dim)
        self.relu = nn.ReLU()
        self.fc2 = nn.Linear(hidden_dim, output_dim)

    def forward(self, x):
        out = self.fc1(x)
        out = self.relu(out)
        out = self.fc2(out)
        return out
```

- `super().__init__()` calls `nn.Module`’s constructor, which sets up parameter tracking.  
- Layers are stored as instance attributes (e.g., `self.fc1`).  
- The `forward` method defines the computation; PyTorch automatically calls it when you do `model(x)`.

If you can explain why `super().__init__()` is needed and what would happen without it, you’re ahead of many candidates.

---

## 🧪 Your Module 3 Exercise (multi-part)

Implement these in real Python (no pseudocode). This will be what you test yourself on later.

### Part 1 – `class MetricTracker`
Write a class that tracks a list of numbers (e.g., loss values per epoch).

- `__init__(self)`: initialise an empty list `self.values`.
- `add(self, value)`: append a value to the list.
- `mean(self)`: return the mean of all values. If no values, return `0.0`.
- `last(self)`: return the last value. If no values, return `None`.

```python
tracker = MetricTracker()
tracker.add(0.8)
tracker.add(0.6)
print(tracker.mean())   # 0.7
print(tracker.last())   # 0.6
```

### Part 2 – inheritance: `class MovingAverageTracker(MetricTracker)`
This tracker doesn’t store all values, only a running average with a momentum factor.

- `__init__(self, momentum=0.9)`: call the parent’s `__init__` (so `self.values` is still created, but you’ll override usage). Store `momentum`, and initialise `self.smoothed = None`.
- Override `add(self, value)`: if `self.smoothed` is `None`, set it to `value`. Otherwise, update:  
  `self.smoothed = momentum * self.smoothed + (1 - momentum) * value`.  
- Add a method `current(self)` that returns `self.smoothed` (or `None` if no data).
- The inherited `mean()` and `last()` will be broken for this subclass (because we don’t store all values). Override them to raise `NotImplementedError` with a clear message.

```python
mat = MovingAverageTracker(0.9)
mat.add(1.0)
mat.add(2.0)
print(mat.current())   # should be close to 1.1 (0.9*1.0 + 0.1*2.0 = 1.1)
```

### Part 3 – Why inheritance? (conceptual, but you’ll write a short explanation)
In 2-3 sentences, explain why inheriting from `MetricTracker` might be useful even though we override almost everything. What would be the alternative, and why might inheritance still be a valid choice?
