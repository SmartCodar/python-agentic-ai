# Lambda Functions & Functional Tools in Python

## Overview
Dive into the world of functional programming in Python. Learn about `lambda` functions and how they power high-order functions like `map()`, `filter()`, `reduce()`, `sorted()`, `min()`, and `max()`. This lesson gives you hands-on mastery over concise function expressions and Python's functional programming capabilities.

## 🎯 Learning Objectives
By the end of this lesson, you will be able to:
- Understand and write Python `lambda` functions
- Use `map()`, `filter()`, `reduce()` with and without lambda
- Apply sorting and aggregation using `sorted()`, `min()`, `max()` with custom keys
- Understand the differences between `list`, `tuple`, `dict`, and `set`
- Debug and refactor lambda-based expressions

## 📋 Prerequisites
- Python 3.11+ installed
- Familiarity with basic Python data types like `list`, `tuple`, `dict`

---

## 1. Theoretical Foundation

### What is a Lambda Function?
A lambda function in Python is an **anonymous function**—a function without a name. It is used to create small, one-line functions quickly without using the `def` keyword.

```python
lambda arguments: expression
```

### When to Use Lambda:
- When a small function is required temporarily
- As an argument to functions like `map()`, `filter()`, `reduce()`, or `sorted()`

> **Note:** Lambda functions are limited to a single expression and cannot contain multiple statements or complex logic.

---

## 2. Core Functional Tools

### 2.1 map(func, iterable)
Applies a function to **each item** in an iterable.

#### Example using lambda:
```python
numbers = [1, 2, 3, 4]
squares = list(map(lambda x: x ** 2, numbers))
print(squares)  # [1, 4, 9, 16]
```

#### Without lambda:
```python
def square(x):
    return x ** 2

squares = list(map(square, [1, 2, 3, 4]))
```

---

### 2.2 filter(func, iterable)
Selects only the items for which the function returns `True`.

#### Using lambda:
```python
numbers = [1, 2, 3, 4, 5]
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # [2, 4]
```

#### Without lambda:
```python
def is_even(x):
    return x % 2 == 0

evens = list(filter(is_even, numbers))
```

---

### 2.3 reduce(func, iterable)
Combines all items into a single value using a specified function. Must be imported from `functools`.

#### Using lambda:
```python
from functools import reduce

numbers = [1, 2, 3, 4]
product = reduce(lambda x, y: x * y, numbers)
print(product)  # 24
```

#### Without lambda:
```python
def multiply(x, y):
    return x * y

product = reduce(multiply, numbers)
```

---

### 2.4 sorted(iterable, key=func)
Returns a new sorted list based on the key function.

#### Using lambda:
```python
words = ["banana", "apple", "cherry"]
sorted_words = sorted(words, key=lambda x: len(x))
print(sorted_words)  # ['apple', 'banana', 'cherry']
```

#### Without lambda:
```python
def word_length(x):
    return len(x)

sorted_words = sorted(words, key=word_length)
```

---

### 2.5 min(), max() with key
Find the smallest or largest item by custom key.

#### Using lambda:
```python
students = [
    {"name": "Alice", "score": 80},
    {"name": "Bob", "score": 92},
    {"name": "Charlie", "score": 70}
]

best_student = max(students, key=lambda x: x["score"])
print(best_student)  # {'name': 'Bob', 'score': 92}
```

#### Without lambda:
```python
def get_score(student):
    return student["score"]

best_student = max(students, key=get_score)
```

---

## 3. Data Type Reference

| Type    | Description               | Example                        |
|---------|---------------------------|--------------------------------|
| `list`  | Ordered, mutable          | `[1, 2, 3]`                    |
| `tuple` | Ordered, immutable        | `(1, 2, 3)`                    |
| `dict`  | Key-value mapping         | `{"a": 1, "b": 2}`             |
| `set`   | Unordered, unique items   | `{"apple", "banana", "apple"}`|

---

## 4. Working with Sets

Sets in Python are collections of **unique**, **unordered** items. They are ideal for membership testing and removing duplicates.

### Examples:
```python
# Creating sets
fruits = {"apple", "banana", "cherry", "apple"}
print(fruits)  # {'banana', 'cherry', 'apple'}

# Add item
fruits.add("mango")

# Set operations
available = {"apple", "banana", "grape"}
requested = {"banana", "mango"}

common = available & requested  # Intersection
all_items = available | requested  # Union
difference = available - requested  # Difference
```

---

## 5. Hands-on Practice

### Exercise 1: Use map and lambda to convert Celsius to Fahrenheit
```python
celsius = [0, 10, 20, 30]
fahrenheit = list(map(lambda c: (9/5)*c + 32, celsius))
print(fahrenheit)  # [32.0, 50.0, 68.0, 86.0]
```

### Exercise 2: Use filter to find names starting with 'A'
```python
names = ["Alice", "Bob", "Amanda", "Mike"]
a_names = list(filter(lambda name: name.startswith('A'), names))
print(a_names)  # ['Alice', 'Amanda']
```

### Exercise 3: Use reduce to compute factorial of a number
```python
from functools import reduce
n = 5
factorial = reduce(lambda x, y: x * y, range(1, n+1))
print(factorial)  # 120
```

---

## 6. Summary

- `lambda` creates one-line anonymous functions  
- `map()` applies a function to all items  
- `filter()` keeps items where the function returns `True`  
- `reduce()` combines all values into one  
- `sorted()`, `min()`, and `max()` can use `key` for custom sorting/comparison  
- `set` is a data structure for storing **unique**, **unordered** elements — useful for filters, uniqueness checks, and comparisons  

These concepts are especially useful in data pipelines, analytics, and competitive programming.

---

## 🔍 Knowledge Check

1. What is the purpose of lambda in `map()`?
2. How does `filter()` behave differently from `map()`?
3. What happens if you use `reduce()` on an empty list?
4. When would you use `set` over `list`?
5. How do `key` functions work in `sorted()` and `min()`?
6. What does `map(lambda x: x * 2, [1, 2, 3])` return?
7. How can `filter()` be used to extract only even numbers from a list?
8. What is the role of `functools.reduce()` in Python?
9. Why is `lambda` preferred in inline function operations?
10. Can you pass multiple iterables to `map()`? What happens?
11. How do you convert a `set` back into a list?
12. What is the time complexity of membership tests in `set` vs `list`?
13. How would you sort a list of strings by their length?
14. What happens if the `key` function returns the same value for all elements?
15. Can you use `lambda` inside a `sorted()` to sort by the last character of a string?
16. How do you eliminate duplicates from a list using a one-liner?
17. What does `sorted(set(mylist))` achieve?
18. What is the default return value of `filter()` when all values are false?
19. How do you calculate the sum of squares using `map()` and `reduce()`?
20. What is the difference between `any()` and `all()` when combined with `filter()` or `map()`?

