# 📘 Python Data Structures for Beginners

This guide explains Python's key data structures — **Tuples**, **Sets**, **Generators**, and **Comprehensions** — in a highly practical and simplified manner. It is designed for **absolute beginners**, especially students or entry-level developers learning Python for the first time.

---

## 🧠 What are Data Structures?

A **data structure** is a way of organizing and storing data so it can be accessed and modified efficiently. In Python, common built-in data structures like **tuples**, **sets**, **lists**, **dictionaries**, and **generators** allow us to write clean and effective programs.

This guide focuses on:
- ✅ Tuples: Fixed-length collections
- ✅ Sets: Unordered collections of unique items
- ✅ Generators: Memory-efficient data pipelines
- ✅ Comprehensions: Shortcuts for creating lists, sets, and dictionaries

---

## 📦 TUPLE

### ✅ Definition
A **tuple** is an **ordered**, **immutable** collection used to group related data. Once created, its content cannot be changed. Tuples are defined using parentheses `()`.

### 🔍 Use Case:
Use a tuple to represent an **employee record** with name, department, and email — values that should not change.

### 💡 Example
```python
employee = ("Amit", "Tech", "ameet@chocosoft.in")
print(employee[0])  # Access name
```

### 🛠️ Common Operations
- Access via index
- Unpack values
- Use as dictionary keys
- Combine tuples

```python
emp_id = (101, "Amit")
record = {emp_id: "Active"}  # Tuple as key
```

---

## 🔁 SET

### ✅ Definition
A **set** is an **unordered collection of unique elements**. It is defined using curly braces `{}` or the `set()` function.

### 🔍 Use Case:
Use a set to track **distinct departments** or **technologies known by team members** — where duplicates don’t make sense.

### 💡 Example
```python
departments = {"Tech", "HR", "Tech"}
print(departments)  # Output: {'Tech', 'HR'}
```

### 🛠️ Common Operations
- Add, remove items
- Perform union, intersection, difference
- Eliminate duplicates from list

```python
tech_stack = {"Python", "AWS"}
print("Python" in tech_stack)
```

---

## ⚙️ GENERATOR

### ✅ Definition
A **generator** is a special type of iterator that **yields one value at a time** using the `yield` keyword. It helps with **efficient memory usage** when dealing with large data.

### 🔍 Use Case:
Use generators to **stream employee IDs**, **process logs**, or **iterate over database rows** without loading everything into memory.

### 💡 Example
```python
def emp_ids():
    for i in range(1, 4):
        yield f"EID{i:03}"

g = emp_ids()
print(next(g))  # 'EID001'
```

### 🛠️ Common Operations
- Define with `yield`
- Use `next()`
- Use in `for` loops
- Replace heavy lists for large datasets

---

## 🧪 COMPREHENSION

### ✅ Definition
Comprehensions provide a **compact syntax** for creating sequences from other iterables using expressions and `for` loops.

### 🔍 Use Case:
Use list comprehensions to **filter employee names**, **generate emails**, or **transform salary records** in one line.

### 💡 Example
```python
names = ["Amit", "Sneha"]
emails = [f"{n.lower()}@zennialpro.com" for n in names]
```

### 🛠️ Types of Comprehension
- List: `[x for x in iterable]`
- Set: `{x for x in iterable}`
- Dict: `{k: v for k, v in iterable}`
- Nested: `[[row for row in matrix] for matrix in data]`

---

## ✅ DOs and DON'Ts

### DO:
- ✅ Use tuples for records (e.g., employee info)
- ✅ Use sets for uniqueness (e.g., tags, skills)
- ✅ Use generators for large or streamed data
- ✅ Use comprehensions for transformation and filtering

### DON'T:
- ❌ Try to modify tuples (they’re immutable)
- ❌ Rely on set order (they’re unordered)
- ❌ Convert large generators into full lists
- ❌ Over-nest comprehensions — keep them readable

---

## 📋 20 Quiz Questions

| # | Question |
|--:|:---------|
| 1 | What data structure is immutable and ordered? |
| 2 | How do you define a set with unique values? |
| 3 | Which structure is best for stream-based processing? |
| 4 | What does `next()` do in a generator? |
| 5 | How do you count an element in a tuple? |
| 6 | Why use a set over a list for lookup operations? |
| 7 | Write a generator to yield square numbers. |
| 8 | How do you filter a list using comprehension? |
| 9 | Can a tuple be used as a dictionary key? |
| 10 | What is the output of `set("banana")`? |
| 11 | What keyword is used to create a generator? |
| 12 | What’s the main difference between list and set? |
| 13 | Which structure saves memory by lazy evaluation? |
| 14 | How do you merge two sets? |
| 15 | Write a comprehension to extract first letter of each name. |
| 16 | What happens if you modify a tuple? |
| 17 | How do you check if an item exists in a set? |
| 18 | What does zip() do? |
| 19 | Can you nest comprehensions? |
| 20 | Why should you avoid overusing nested comprehensions? |

---
