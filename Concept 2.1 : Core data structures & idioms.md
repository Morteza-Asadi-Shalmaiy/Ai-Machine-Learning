# Concept 1 : Core data structures & idioms
Lists, dicts, tuples, sets, comprehensions, slicing, unpacking. <br> 
For the purpose of baseline fluency. Every ML coding question sits on top of this. if you are Weak here = slow and clunky everywhere else.

---

## Module 1 — Teaching: Core Data Structures & Idioms (ML-relevant subset)

### 1. Lists
- Ordered, mutable, allow duplicates.
- Used for sequences of samples, token IDs, batch indices, feature columns.
- Common ops: `append`, `extend`, indexing, slicing, list comprehensions.
Great question — let's make sure lists are crystal clear before you tackle the exercise.

---

## What is a list in Python?

A **list** is an ordered, mutable (changeable) collection of items. You can put anything inside: numbers, strings, other lists, etc. In ML, you'll use lists constantly — to hold a batch of token IDs, a sequence of predictions, rows of a CSV, etc.

**Key characteristics:**
- **Ordered** — items stay in the order you add them.
- **Mutable** — you can add, remove, or change items after creation.
- **Allow duplicates** — the same value can appear many times.
- **Indexable** — you access items by their position (0‑based).

---

## Creating a list
```python
# empty list
empty = []

# list of integers
predictions = [2, 0, 2, 1, 0]

# mixed types (rarely used in serious ML, but possible)
mixed = [3, "cat", 2.5]

# list from range
nums = list(range(5))   # [0, 1, 2, 3, 4]
```

---

## Basic operations you'll use in ML

```python
preds = [2, 0, 1]

# Access by index
first = preds[0]        # 2
last  = preds[-1]       # 1

# Slicing (sub‑list)
first_two = preds[:2]   # [2, 0]

# Add items
preds.append(3)         # now [2, 0, 1, 3]
preds.extend([4, 5])    # [2, 0, 1, 3, 4, 5]

# Modify an item
preds[1] = 9            # [2, 9, 1, ...]

# Remove
preds.remove(9)         # removes first occurrence of 9
popped = preds.pop()    # removes & returns last item

# Length
len(preds)              # number of elements

# Check membership
2 in preds              # True

# Iterate (loop)
for p in preds:
    print(p)
```

---

## Why lists matter for ML interviews
- You'll often be given raw Python data (like `predictions` and `labels`) and asked to compute metrics without NumPy.
- List comprehensions are a Pythonic way to transform lists quickly:
  ```python
  squares = [x**2 for x in range(5)]   # [0, 1, 4, 9, 16]
  ```
- Slicing is how you'd manually implement mini‑batch extraction.
- Lists underpin the concepts you'll later vectorize with NumPy.

---

### 2. Tuples
- Ordered, **immutable**, often used for fixed collections: `(height, width)`, coordinates, `(X_train, y_train)` returns from `train_test_split`.
- Unpacking: `x, y = (3, 4)` → clean multi‑return assignments.
- Key ML usage: function return multiple values; dictionary keys when you need a composite key that's hashable.
## Tuples in Python (ML‑focused)

A **tuple** is similar to a list: it's an ordered collection of items. The big difference? Tuples are **immutable** — once you create one, you cannot change, add, or remove elements.

### Why tuples matter in ML code:
- **Multiple return values** — many functions return a pair like `(X_train, y_train)`. You can unpack them immediately:  
  `X_train, y_train = train_test_split(X, y)`
- **Fixed configurations** — image sizes `(224, 224)`, color channels `(3,)`, coordinate points — data that shouldn't change.
- **Dictionary keys** — because they're immutable and hashable, tuples can be used as keys in a dict (e.g., `{("cat", "dog"): 0.8}` for pairwise similarity).
- **Memory efficiency** — slightly smaller and faster than lists when you don't need mutation.

### Creating tuples
```python
# Using parentheses (the standard way)
shape = (224, 224, 3)

# Without parentheses — just commas (tuple packing)
shape2 = 224, 224, 3      # same as above

# Single‑element tuple — the comma is crucial
single = (3,)              # not (3), which is just the integer 3
```

### Unpacking (the most useful feature for you)
```python
# Unpack a tuple into variables
height, width, channels = shape   # height=224, width=224, channels=3

# Swapping variables without a temp variable
a, b = 1, 2
a, b = b, a   # a=2, b=1

# Capturing the rest (like *args, but on a tuple)
first, *others = (10, 20, 30, 40)   # first=10, others=[20,30,40]
```

### Common operations
```python
t = (0, 1, 2, 1)

# Indexing & slicing (just like lists)
t[0]        # 0
t[1:3]      # (1, 2)

# Check membership
1 in t      # True

# Count occurrences & find index
t.count(1)  # 2
t.index(2)  # 2

# Concatenation, repetition
t + (3, 4)  # (0,1,2,1,3,4)
t * 2       # (0,1,2,1,0,1,2,1)

# Length
len(t)      # 4
```

### Immutability in action
```python
t = (1, 2, 3)
t[0] = 5   # ❌ TypeError: 'tuple' object does not support item assignment
```
You can't change a tuple, but if a tuple contains a mutable object (like a list), that inner object *can* be changed — but that's a finer point we'll skip for now.

### Tuple vs list in ML code
- If you have a collection that shouldn't accidentally be modified (model hyperparameters, data splits), use a tuple.
- If you need to add/remove items (gathering predictions, building a batch), use a list.

### How this connects to our exercise
In the exercise, you might return a tuple from `prediction_mode` (the frequency and the mode list) — `(max_freq, modes_list)` is a perfect tuple use case. You also might unpack the results when you print them.

---


### 3. Dictionaries (dicts)
- Key‑value, hashable keys.
- ML usage: label mapping (`{"cat": 0, "dog": 1}`), model hyperparameter configs, counting frequencies (`collections.Counter`), caching.
- Comprehension: `{k: v for k, v in ...}`.
## Dictionaries (dicts) in Python — the key‑value powerhouse

A **dictionary** is an unordered (but insertion‑ordered in Python 3.7+) collection of **key‑value pairs**. You look up a value by its key — like a real dictionary where you look up a word (key) to find its definition (value).

In ML code, dictionaries are everywhere:

### Why dictionaries matter for ML
- **Label mappings:** map class indices to human‑readable names: `{0: "cat", 1: "dog", 2: "bird"}`
- **Hyperparameter configs:** `{"learning_rate": 0.001, "epochs": 10, "batch_size": 32}`
- **Counting frequencies:** how many times each class appears in a dataset (we'll use this in the exercise's `prediction_mode`).
- **Caching / memoization:** store computed results so you don't recalculate them.
- **Feature dictionaries:** data samples often come as `{"feature1": value, "feature2": value}`.

### Key characteristics
- **Mutable** — you can add, remove, and change pairs after creation.
- **Keys must be hashable** — that means immutable types like strings, numbers, tuples. Lists cannot be keys.
- **Values can be anything** — lists, other dicts, functions, whatever.
- **Fast lookups** — finding a value by key is very fast, no matter how big the dictionary.

### Creating a dictionary
```python
# Empty dict
empty = {}

# With initial pairs
class_to_name = {0: "cat", 1: "dog", 2: "bird"}

# Using dict() constructor with keyword arguments (keys become strings)
config = dict(learning_rate=0.001, epochs=10)

# From a list of tuples
pairs = [(0, "cat"), (1, "dog")]
class_map = dict(pairs)   # {0: "cat", 1: "dog"}
```

### Basic operations
```python
mapping = {0: "cat", 1: "dog"}

# Access a value (KeyError if key missing)
mapping[0]                # "cat"

# Safely get a value with a default
mapping.get(2, "unknown") # "unknown"

# Add or update a pair
mapping[2] = "bird"       # now {0:"cat", 1:"dog", 2:"bird"}
mapping[0] = "feline"     # update existing key

# Remove a key
del mapping[2]
# or pop a key to get its value and remove it
val = mapping.pop(1)      # "dog", now mapping = {0:"cat"}

# Check if a key exists
0 in mapping              # True

# Iterate over keys, values, or both
for k in mapping.keys():      # or just `for k in mapping:`
    print(k)
for v in mapping.values():
    print(v)
for k, v in mapping.items():
    print(f"{k} -> {v}")

# Length
len(mapping)              # number of key-value pairs
```

### Dict comprehensions — a concise way to build dictionaries
```python
# Example: square numbers
squares = {x: x**2 for x in range(5)}   # {0:0, 1:1, 2:4, 3:9, 4:16}

# ML example: create a mapping from index to name for selected classes
unique_indices = [0, 2]
names = ["cat", "dog", "bird"]
name_map = {i: names[i] for i in unique_indices}   # {0:"cat", 2:"bird"}
```
This is exactly what you'll need in the exercise, task 2.

### Counting with dictionaries (very ML‑relevant)
```python
predictions = [2, 0, 2, 1, 0]
counts = {}
for p in predictions:
    if p in counts:
        counts[p] += 1
    else:
        counts[p] = 1
# counts = {2:2, 0:2, 1:1}
```
A more elegant way with `get`:
```python
counts = {}
for p in predictions:
    counts[p] = counts.get(p, 0) + 1
```
This pattern is central to the `prediction_mode` function in the exercise.

### How dictionaries connect to the exercise
- Task 2: you'll use a **dict comprehension** to create `{index: class_name}`.
- Task 4: you'll use a dictionary to count prediction frequencies, then find the max.

---


### 4. Sets
- Unordered, unique elements, hashable.
- ML usage: remove duplicates (unique classes in a label column), fast membership tests, set operations on experiment IDs.
- Set comprehensions: `{x for x in ... if ...}`.
## Sets in Python — the uniqueness enforcer

A **set** is an unordered collection of **unique** elements. No duplicates, and like dictionary keys, elements must be hashable (immutable types like numbers, strings, tuples).

### Why sets matter in ML
- **Unique classes:** extract all distinct labels from a target column — exactly what task 1 in your exercise asks.
- **Membership tests:** fast check if an element exists (e.g., `id in visited_ids`).
- **Set operations:** compare train and test labels to find unseen classes, or find common experiments.
- **Remove duplicates** from any iterable instantly.

### Key characteristics
- **Mutable** (but elements must be immutable). There's also `frozenset` for immutable sets, but we'll skip that.
- **No guaranteed order** — in Python 3.7+ they happen to preserve insertion order (like dicts), but you shouldn't rely on that; use `sorted()` for consistent output.
- **Cannot access by index** — no `s[0]`. You iterate over them.

### Creating a set
```python
# From a list (duplicates vanish)
labels = [2, 0, 2, 1, 0]
unique = set(labels)       # {0, 1, 2}

# Empty set (careful: {} is a dict)
empty = set()

# Set comprehension
squared = {x**2 for x in range(5) if x % 2 == 0}  # {0, 4, 16}
```

### Basic operations
```python
s = {0, 1, 2}

# Add/remove
s.add(3)          # {0,1,2,3}
s.remove(3)       # KeyError if missing
s.discard(5)      # no error if missing

# Membership (very fast)
1 in s            # True

# Length
len(s)            # 3

# Iterate
for elem in s:
    print(elem)
```

### Set operations (Venn diagram style)
```python
a = {0, 1, 2}
b = {1, 2, 3}

a | b   # union: {0,1,2,3}
a & b   # intersection: {1,2}
a - b   # difference: {0}
a ^ b   # symmetric difference: {0,3}
```
These are useful for comparing experiment IDs, feature sets, or class labels across splits.

### How this connects to the exercise
- Task 1 explicitly asks: "Use a set to ensure uniqueness." Convert the `labels` list to a set, then `sorted()` to return a sorted list.

---


### 5. Comprehensions
- Concise, efficient way to build lists/dicts/sets from an iterable.
- List comprehension: `[transform(x) for x in data if condition]`
- Dict comprehension: `{sample_id: label for sample_id, label in zip(ids, labels)}`
- Set comprehension: `{pred for pred in predictions if pred != -1}`
Got it — you want me to re-explain **number 5: Comprehensions**, more clearly. No problem.

---

## Comprehensions — the simple idea

A comprehension is just a **shortcut** for building a new list (or dict, or set) from an existing sequence, while maybe filtering some items or changing each item.

Instead of writing a full for‑loop with `.append()`, you do it all in one line.

### Analogy
Imagine you have a basket of apples. You want a new basket with **only the red apples**, but **each one peeled**.
- Without comprehension: you pick up each apple, check if red, peel it, place it in new basket.
- With comprehension: `[peel(apple) for apple in basket if is_red(apple)]` — same logic, one line.

---

### List comprehension — the most common
Basic pattern:
```python
new_list = [do_something(item) for item in old_list]
```

**Example with numbers:**
```python
nums = [1, 2, 3, 4]
doubled = [x * 2 for x in nums]      # [2, 4, 6, 8]
```

With **filtering** (only if condition is true):
```python
evens = [x for x in nums if x % 2 == 0]   # [2, 4]
```

With **both**:
```python
odd_squared = [x**2 for x in nums if x % 2 == 1]   # [1, 9]
```

### Dict comprehension
Same idea, but you produce **key: value** pairs:
```python
names = ["cat", "dog", "bird"]
# Map index -> name
index_map = {i: names[i] for i in range(len(names))}
# {0: "cat", 1: "dog", 2: "bird"}
```

With filtering:
```python
# Only include indices where name length > 3
{ i: names[i] for i in range(len(names)) if len(names[i]) > 3 }
# {2: "bird"}
```

### Set comprehension
Produces a set (unique values):
```python
words = ["cat", "dog", "cat", "bird"]
unique = {w for w in words}   # {"cat", "dog", "bird"}
```

---

### How this connects to your exercise

- **Task 1 (unique classes)** — you can just use `set(labels)` directly, no comprehension needed. But a set comprehension `{label for label in labels}` gives the same result.
- **Task 2 (name mapping)** — a dict comprehension is perfect:
  ```python
  {index: class_names[index] for index in unique_indices}
  ```
  This reads as: "for each index in `unique_indices`, make a key-value pair with `index` as key and `class_names[index]` as the value."
- **Task 3 (confusion row)** — a list comprehension can count matches:
  ```python
  [sum(1 for true, pred in zip(labels, predictions) if true == k and pred == class_j) for class_j in unique_classes]
  ```
  This one is trickier; a simple loop is fine too.
- **Task 4 (most frequent)** — not strictly a comprehension, but you can build the frequency dict with a comprehension using `counts.get()`? No, easier with loop.
- **Task 5 (batch)** — just slicing, no comprehension.

---

### 6. Slicing
- `sequence[start:stop:step]` — works on lists, tuples, strings, NumPy arrays (later).
- Frequently used in ML: train/val/test splits, batch extraction, first N tokens, last N layers.
## Slicing in Python — extracting subsequences

Slicing is a way to pull out a portion of a sequence (list, tuple, string, etc.) using the syntax:

```python
sequence[start : stop : step]
```

- **start** – index to begin (inclusive). Defaults to `0` if omitted.
- **stop** – index to end (exclusive). Defaults to the end of the sequence if omitted.
- **step** – stride between elements. Defaults to `1`.

All three are optional. You can use negative indices to count from the end.

### Basic examples with a list
```python
data = [10, 20, 30, 40, 50, 60]

# First three elements
data[0:3]   # [10, 20, 30]
data[:3]    # same

# From index 2 to the end
data[2:]    # [30, 40, 50, 60]

# Last two elements
data[-2:]   # [50, 60]

# Every second element
data[::2]   # [10, 30, 50]

# Reverse a list
data[::-1]  # [60, 50, 40, 30, 20, 10]
```

### Why slicing is crucial in ML
- **Mini‑batch extraction:** `batch = data[start:start+batch_size]` — exactly your Task 5.
- **Train/val/test splits:** `train = data[:80%]`, `val = data[80%:90%]`, `test = data[90%:]`
- **Sequence truncation:** take first 512 tokens from a long text.
- **Selecting top‑K predictions or features:** `topk = sorted_preds[:5]`

### Task 5 from your exercise uses slicing directly
```python
def get_batch(predictions, labels, start, batch_size):
    return predictions[start:start+batch_size], labels[start:start+batch_size]
```
Python automatically handles the case where `start+batch_size` exceeds the length — it just stops at the end.

### Slicing works on tuples, strings, and later NumPy arrays, too
```python
shape = (224, 224, 3)
h, w = shape[:2]   # (224, 224)

s = "machine learning"
s[:7]              # "machine"
```

---


### 7. Unpacking
- `a, b = [1, 2]`; `*rest` for the remainder: `first, *others = list`.
- Appears in `*args, **kwargs` (Module 2), handling variable‑length model inputs, and looping over batches: `for x_batch, y_batch in dataloader`.
## Unpacking in Python — pulling values apart

Unpacking means taking a sequence (list, tuple, etc.) and assigning its elements to separate variables in one go. It's the opposite of packing.

### Basic unpacking
```python
pair = (224, 224)        # a tuple
height, width = pair     # height = 224, width = 224

# Works with lists too
rgb = [255, 0, 128]
r, g, b = rgb            # r=255, g=0, b=128
```

The number of variables on the left must match the length of the sequence, otherwise you'll get a `ValueError`.

### In ML code, you see this constantly
```python
# sklearn returns a tuple
X_train, X_test, y_train, y_test = train_test_split(X, y)

# Enumerate gives index-value pairs
for i, label in enumerate(labels):
    print(i, label)

# Looping over DataLoader yields (batch_X, batch_y)
for x_batch, y_batch in dataloader:
    ...
```

### Extended unpacking with `*` (starred expressions)
You can capture "the rest" with a `*`:
```python
first, *middle, last = [10, 20, 30, 40, 50]
# first = 10, middle = [20, 30, 40], last = 50
```

Useful when you have a variable‑length sequence and only need some parts.

### Unpacking into function arguments (preview of Module 2)
```python
config = {"lr": 0.01, "epochs": 5}
train(**config)   # passes lr=0.01, epochs=5 as keyword arguments
```
This is `**kwargs` territory — you'll learn it soon.

### In your exercise
Unpacking can be handy:
- When you call your `prediction_mode` and get `(freq, modes)`, you can unpack:
  ```python
  freq, mode_list = prediction_mode(predictions)
  ```
- Or when iterating over `zip(labels, predictions)` to get true and pred pairs.

---

# CheatSheet 

Here's your **Module 1 Cheat Sheet** — a quick-reference card to review right before the interview. Keep it handy.

---

## 🐍 Python Data Structures & Idioms — ML Interview Cheat Sheet

| Structure | Ordered? | Mutable? | Duplicates? | Create | Common ML Use |
|-----------|----------|----------|-------------|--------|----------------|
| **list**  | Yes      | Yes      | Yes         | `[ ]` or `list()` | Batch tokens, predictions, column values |
| **tuple** | Yes      | No       | Yes         | `( )` or `,` | Fixed configs, multiple returns, dict keys |
| **dict**  | Ins. order¹| Yes    | Keys unique | `{ : }` or `dict()` | Label mapping, configs, frequency counting |
| **set**   | Ins. order¹| Yes    | No          | `{ }` (no `:`) or `set()` | Unique classes, fast membership tests |

¹ Insertion order preserved in Python 3.7+.

### 1. Lists
```python
preds = [2, 0, 1]
preds.append(3)            # add to end
preds.extend([4,5])        # extend with another iterable
preds[0] = 9               # change by index
len(preds)                 # length
3 in preds                 # membership
for p in preds: ...        # iterate
```

### 2. Tuples
```python
shape = (224, 224, 3)      # packing
h, w, c = shape            # unpacking
first, *rest = (1,2,3,4)   # extended unpacking: first=1, rest=[2,3,4]
a, b = b, a                # swap
# tuple as dict key (hashable)
coords = {(x, y): value}
```

### 3. Dictionaries
```python
class_map = {0: "cat", 1: "dog"}
class_map[2] = "bird"         # add/update
class_map.get(2, "unknown")   # safe access with default
del class_map[0]              # delete
class_map.pop(1)              # remove and return value
for k, v in class_map.items(): # iterate keys & values
```
**Counting pattern:**
```python
counts = {}
for p in predictions:
    counts[p] = counts.get(p, 0) + 1
```

### 4. Sets
```python
unique = set(labels)           # from list
s = {0, 1, 2}
s.add(3)
s.remove(3)          # KeyError if missing
s.discard(5)         # no error if missing
# Set operations
a | b   # union
a & b   # intersection
a - b   # difference
```

### 5. Comprehensions (list / dict / set)
```python
# List comprehension
[x**2 for x in range(5)]                          # [0,1,4,9,16]
[p for p in preds if p != -1]                     # filter

# Dict comprehension
{i: class_names[i] for i in unique_indices}       # map index -> name

# Set comprehension
{label for label in labels}                       # unique labels
```

### 6. Slicing
```python
seq[start:stop:step]
seq[:3]       # first 3
seq[2:]       # from index 2 to end
seq[-2:]      # last 2
seq[::2]      # every 2nd
seq[::-1]     # reversed
```
**ML usage:** `batch = data[start:start+batch_size]`

### 7. Unpacking
```python
x, y = (3, 4)               # tuple unpacking
first, *rest = [1,2,3,4]    # rest = [2,3,4]
for i, val in enumerate(vals):  # enumerate returns index,value
```

**Instant ML application:**
```python
X_train, X_test, y_train, y_test = train_test_split(X, y)  # unpack tuple
```
