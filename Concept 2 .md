# Python Prep Roadmap — AI Engineer Interview (1-2 weeks)

**Scope:** ML/AI-relevant Python only. No generic algorithm puzzles (sorting, graph traversal, DP) unless you tell me the round is generic SWE-style.

**Your level:** Python beginner.

**Companion track:** ML/AI theory (separate conversation) — bias-variance, regularization, metrics, RF vs GBM, leakage, then PyTorch/LLMs/deployment.

---

## How each session works

1. **Teach** — short, focused concept explanation (no fluff).
2. **Exercise** — a practical, often multi-part task. Multi-part on purpose: interviewers expect you to answer the *whole* question, not stop at the first sub-point or a one-word diagnosis.
3. **Evaluate** — I grade your actual code like an interviewer would:
   - What's correct
   - What's missing or fragile (edge cases, inefficiency, style)
   - A score (/10)
   - Follow-up pressure if you stopped short
4. **Move on** once you've hit a solid bar — not perfection, but "would pass an interview" level.

You write real code every time. I don't accept pseudocode or "I think I'd do X" — same standard as a live coding round.

---

## The 6 Modules (in order)

| # | Module | Why it's tested |
|---|--------|------------------|
| 1 | **Core data structures & idioms** — lists, dicts, tuples, sets, comprehensions, slicing, unpacking | Baseline fluency. Every ML coding question sits on top of this. Weak here = slow and clunky everywhere else. |
| 2 | **Functions** — default args, `*args`/`**kwargs`, lambdas | Shows up constantly in ML code (`sorted(key=lambda...)`, flexible configs, wrapping model calls). |
| 3 | **OOP basics** — classes, `__init__`, inheritance | Directly mirrors PyTorch's `nn.Module` pattern (`class Model(nn.Module): def __init__(self): super().__init__()...`). If this is shaky, PyTorch will feel like magic instead of mechanics. |
| 4 | **NumPy fundamentals** — vectorization, broadcasting, indexing | Classic interview move: "here's a slow loop, vectorize it." Also underlies almost all data preprocessing. |
| 5 | **ML-flavored coding exercises** — sigmoid, softmax, accuracy/precision/F1 from scratch, small data manipulation tasks | The bread-and-butter "write a function" round for ML-specific interviews. Tests whether you understand the math *and* can implement it cleanly. |
| 6 | **Generators/iterators (lightweight)** | Underlies PyTorch `DataLoader`/`Dataset` — understanding `__iter__`/`__next__`/`yield` demystifies how batching works under the hood. |

---

## Ground rules

- **No skipping to the label.** If asked "what's wrong with this code" or "what metric would you use," a one-word answer isn't enough — I'll push for the full reasoning, tradeoffs, and a concrete fix/example, same as a real interviewer would.
- **Beginner-paced, not beginner-scoped.** We won't skip anything relevant just because it's your first time — we'll just take the time to build it up properly.
- We only move to the next module once you're consistently scoring at a "pass" level on the current one — not necessarily 10/10, but solid.
- If you want, at the end we can do a **mock timed exercise** mixing modules 1, 4, and 5, since that combo is the most realistic simulation of an actual live coding round.

---

# Module Starter Prompts — Python Interview Prep

Paste the relevant prompt into this conversation whenever you're ready to start (or resume) that module. Each one is self-contained and tells me exactly how to coach you.

---

## Module 1: Core Data Structures & Idioms

Start Module 1: Core Data Structures & Idioms.

Coach me on Python core data structures & idioms — lists, dicts, tuples, sets, comprehensions, slicing, unpacking — as prep for a mid-level AI Engineer interview. I'm a Python beginner.

Teach the concept first, then give me a practical (ideally multi-part) exercise. When I answer, grade it like a real interviewer: what's correct, what's missing or fragile, a score out of 10, and push me if I stop at a shallow/label-level answer instead of fully working through it. Don't move on until I'm consistently passing.

---

## Module 2: Functions

Start Module 2: Functions.

Coach me on Python functions — default args, *args/**kwargs, and lambdas — as prep for a mid-level AI Engineer interview. I'm a Python beginner. Assume I've already covered core data structures (Module 1).

Teach the concept first, then give me a practical (ideally multi-part) exercise, focused on how these show up in ML code (e.g. flexible config functions, sorted(key=lambda...), wrapping model calls). When I answer, grade it like a real interviewer: what's correct, what's missing or fragile, a score out of 10, and push me if I stop at a shallow/label-level answer. Don't move on until I'm consistently passing.

---

## Module 3: OOP Basics

Start Module 3: OOP Basics.

Coach me on Python OOP basics — classes, __init__, inheritance — as prep for a mid-level AI Engineer interview. I'm a Python beginner. Assume I've covered data structures and functions (Modules 1-2).

Teach the concept first, explicitly connecting it to PyTorch's nn.Module pattern (class Model(nn.Module): def __init__(self): super().__init__()...) since that's why this matters for my interview. Then give me a practical (ideally multi-part) exercise. When I answer, grade it like a real interviewer: what's correct, what's missing or fragile, a score out of 10, and push me if I stop at a shallow/label-level answer. Don't move on until I'm consistently passing.

---

## Module 4: NumPy Fundamentals

Start Module 4: NumPy Fundamentals.

Coach me on NumPy fundamentals — vectorization, broadcasting, indexing — as prep for a mid-level AI Engineer interview. I'm a Python beginner. Assume I've covered data structures, functions, and OOP (Modules 1-3).

Teach the concept first, then give me a practical exercise, ideally including a "here's a slow Python loop, vectorize it with NumPy" style task since that's a classic interview question. When I answer, grade it like a real interviewer: what's correct, what's missing (e.g. did I actually use broadcasting/vectorization or just hide the loop), a score out of 10, and push me if I stop at a shallow/label-level answer. Don't move on until I'm consistently passing.

---

## Module 5: ML-Flavored Coding Exercises

Start Module 5: ML-Flavored Coding Exercises.

Coach me on writing small ML-related functions from scratch — sigmoid, softmax, accuracy/precision/F1, and small data manipulation tasks — as prep for a mid-level AI Engineer interview. I'm a Python beginner. Assume I've covered data structures, functions, OOP, and NumPy (Modules 1-4).

Teach each concept briefly (the math + why it's implemented that way), then give me a practical exercise to implement it in Python/NumPy. When I answer, grade it like a real interviewer: correctness, edge cases (e.g. numerical stability in sigmoid/softmax, zero-division in precision/F1), a score out of 10, and push me if I stop at a shallow/label-level answer instead of fully implementing and testing it. Don't move on until I'm consistently passing.

---

## Module 6: Generators/Iterators (Lightweight)

Start Module 6: Generators/Iterators.

Coach me on Python generators and iterators — yield, __iter__, __next__ — as prep for a mid-level AI Engineer interview. I'm a Python beginner. Assume I've covered data structures, functions, OOP, NumPy, and ML-flavored exercises (Modules 1-5).

Teach the concept first, explicitly connecting it to how PyTorch's DataLoader/Dataset pattern works under the hood, since that's why this matters for my interview. Then give me a practical (ideally multi-part) exercise. When I answer, grade it like a real interviewer: what's correct, what's missing or fragile, a score out of 10, and push me if I stop at a shallow/label-level answer. Don't move on until I'm consistently passing.

