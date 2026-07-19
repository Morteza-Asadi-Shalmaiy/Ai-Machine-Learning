# Concept 1 : Core data structures & idioms
Lists, dicts, tuples, sets, comprehensions, slicing, unpacking. <br> 
For the purpose of baseline fluency. Every ML coding question sits on top of this. if you are Weak here = slow and clunky everywhere else.

---

## Module 1 — Teaching: Core Data Structures & Idioms (ML-relevant subset)

### 1. Lists
- Ordered, mutable, allow duplicates.
- Used for sequences of samples, token IDs, batch indices, feature columns.
- Common ops: `append`, `extend`, indexing, slicing, list comprehensions.

### 2. Tuples
- Ordered, **immutable**, often used for fixed collections: `(height, width)`, coordinates, `(X_train, y_train)` returns from `train_test_split`.
- Unpacking: `x, y = (3, 4)` → clean multi‑return assignments.
- Key ML usage: function return multiple values; dictionary keys when you need a composite key that's hashable.

### 3. Dictionaries (dicts)
- Key‑value, hashable keys.
- ML usage: label mapping (`{"cat": 0, "dog": 1}`), model hyperparameter configs, counting frequencies (`collections.Counter`), caching.
- Comprehension: `{k: v for k, v in ...}`.

### 4. Sets
- Unordered, unique elements, hashable.
- ML usage: remove duplicates (unique classes in a label column), fast membership tests, set operations on experiment IDs.
- Set comprehensions: `{x for x in ... if ...}`.

### 5. Comprehensions
- Concise, efficient way to build lists/dicts/sets from an iterable.
- List comprehension: `[transform(x) for x in data if condition]`
- Dict comprehension: `{sample_id: label for sample_id, label in zip(ids, labels)}`
- Set comprehension: `{pred for pred in predictions if pred != -1}`

### 6. Slicing
- `sequence[start:stop:step]` — works on lists, tuples, strings, NumPy arrays (later).
- Frequently used in ML: train/val/test splits, batch extraction, first N tokens, last N layers.

### 7. Unpacking
- `a, b = [1, 2]`; `*rest` for the remainder: `first, *others = list`.
- Appears in `*args, **kwargs` (Module 2), handling variable‑length model inputs, and looping over batches: `for x_batch, y_batch in dataloader`.

---

## Practical Exercise (multi‑part)

**Context:** You've extracted some predictions from a model and have associated ground‑truth labels. You need to process them for evaluation and reporting. We'll implement a few utility functions using the structures above. Write actual Python code (no pseudocode). Assume standard Python, no imports except maybe `math` if needed, but you won't need it.

**Data you'll work with** (given in the function calls):
```python
predictions = [2, 0, 2, 1, 0, 2, 1, 0]
labels      = [2, 1, 0, 1, 0, 2, 1, 0]
class_names = ["cat", "dog", "bird"]   # index -> name
```

**Tasks:**

1. **Unique classes in labels:** Write a function `unique_classes(labels)` that returns a sorted list of the unique class indices present. Use a set to ensure uniqueness.

2. **Class name mapping:** Write a function `get_class_names_mapping(unique_indices, class_names_list)` that returns a dictionary mapping each class index to its name (string). Only include indices that actually appear in `unique_indices`. Use a dict comprehension.

3. **Confusion matrix row counts (simplified):** A "confusion matrix row" for a given true class `k` is a list of counts of how often each predicted class appears when the true label is `k`. Write a function `confusion_row(k, labels, predictions)` that returns a list `counts` of length `num_classes` (the number of unique classes in `labels`), where `counts[j]` = number of times true label = `k` and predicted label = class `j`. You can assume classes are 0‑indexed integers and `num_classes` is max(labels)+1 for simplicity, but let's use the sorted unique classes to determine the indexing (i.e., if unique classes are [0,1,2], then index 0 corresponds to class 0, index 1 to class 1, index 2 to class 2). Essentially, map the class integer directly to its list index (since classes are contiguous integers 0..C-1). Use list operations (comprehension or manual loop) — no NumPy (that's later). The output for `k=0` with the data above should be: `[3, 0, 0]`? Let's verify: True label 0 appears at indices 1,4,7. Predictions at those positions: index1=0, index4=0, index7=0 — all 0, so count for predicted class 0 is 3, others 0. So `[3, 0, 0]`.

4. **Top‑K most frequent prediction:** Find the most frequent prediction(s) and return a tuple `(frequency, list_of_modes)` sorted ascending. Use dictionary counting. For the given `predictions`, which value(s) appear most often? Predictions: 2 appears three times (indices 0,2,5), 0 appears three times (1,4,7), 1 appears two times (3,6). So the mode frequency is 3, and modes are [0,2]. Function signature: `prediction_mode(predictions)` → `(max_freq, modes_list)`.

5. **Slice‑based batch sampling:** Simulate taking the first `batch_size` predictions/labels pairs for a mini‑batch. Write a function `get_batch(predictions, labels, start, batch_size)` that returns a tuple of two lists: `(pred_batch, label_batch)` using slicing. Assume `start` is an integer index. If `start + batch_size` exceeds the length, the slice should just go to the end (Python slicing handles this automatically, so you don't need extra checks). Example: `get_batch(predictions, labels, 0, 3)` → `([2,0,2], [2,1,0])`.

**Write all functions in a single code block. Include a simple test using the provided data, printing results for each function.**

Now write your code. I'll grade it like an interviewer: correctness, edge‑case handling, style, and will push you if you stopped short. Don't worry about being perfect — just write real code.
