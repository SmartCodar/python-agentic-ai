
# ✅ Python Variables & Data Types Guide

## 📖 Introduction

In Python, **variables** are used to store data, and **data types** define what kind of data is stored. Understanding these two concepts is fundamental for writing efficient and bug-free Python code.

---

## 🎯 Variables in Python

### ✅ What is a Variable?

A **variable** in Python is a reserved memory location used to store values. Python is **dynamically typed**, meaning you do not need to declare the type of variable before using it.

### ✅ Naming Conventions (PEP-8)

- Variable names should be lowercase, with words separated by underscores (`snake_case`).
- Avoid using reserved keywords.

### ✅ Variable Declaration Examples

```python
name = "Amit"
age = 30
salary = 45000.50
is_employed = True
```

### ✅ Multiple Assignments

```python
x, y, z = 10, 20, 30
a = b = c = "Same Value"
```

### ✅ Swapping Variables

```python
x, y = y, x
```

---

## 📊 Python Data Types

### ✅ Primitive Data Types

| Type  | Example                  | Description                          |
|-------|--------------------------|---------------------------------------|
| int   | `a = 10`                 | Integer numbers                      |
| float | `b = 10.5`               | Decimal numbers                      |
| str   | `name = "Amit"`          | String of characters                 |
| bool  | `status = True`          | Boolean value (`True` or `False`)    |

### ✅ Composite Data Types

| Type  | Example                          | Description                          |
|-------|-----------------------------------|---------------------------------------|
| list  | `fruits = ['apple', 'mango']`   | Ordered, mutable collection          |
| tuple | `coordinates = (10, 20)`        | Ordered, immutable collection        |
| dict  | `user = {'name': 'Amit'}`       | Key-value pairs                      |
| set   | `unique_ids = {1, 2, 3}`        | Unordered, unique elements           |

---

## 🧪 Type Checking and Conversion

### ✅ Type Checking

```python
print(type(10))        # <class 'int'>
print(type("Amit"))    # <class 'str'>
```

### ✅ Type Casting / Conversion

```python
x = "100"
print(int(x))          # 100
print(float(x))        # 100.0
```

---

## 🚀 Mutable vs Immutable Types

| Type Category | Data Types                    | Example                               |
|----------------|-----------------------------|----------------------------------------|
| Immutable      | int, float, str, tuple, bool | Cannot change in place                |
| Mutable        | list, dict, set              | Can be changed in place               |

---

## 🎓 Real-World Use Cases

| Scenario              | Example                               | Use Case                            |
|------------------------|----------------------------------------|--------------------------------------|
| API Responses          | `dict`                                | Structured data via JSON             |
| User Input             | `str`, `int`                          | Collecting and validating data       |
| Data Aggregation       | `list`, `set`                         | Storing and deduplicating items      |
| Coordinates Handling   | `tuple`                                | Immutable storage of coordinates     |

---

## 🧠 Summary

- Python uses **dynamic typing** for flexible variable handling.
- Built-in **primitive** and **composite** data types.
- Use `type()` to check data type and `int()`, `str()`, etc., to convert between types.

---

## 🔍 Quiz Time

1. What is dynamic typing in Python?
2. Name four primitive data types in Python.
3. How do you declare multiple variables in one line?
4. Which data type would you use to store coordinates?
5. What function is used to check a variable's data type?
6. How can you convert a string `"100"` to an integer?
7. Which data types are mutable?
8. Give an example of swapping variables in Python.
9. What is the main difference between `list` and `tuple`?
10. Why is it useful to know mutable vs immutable types?
11. Which data type is commonly used for JSON responses?
12. How do you store unique elements in Python?
13. What is the syntax to declare a dictionary?
14. How would you store multiple user inputs?
15. Explain `type casting` with an example.
16. Can you assign the same value to multiple variables? How?
17. What is the significance of PEP-8 in variable naming?
18. How to swap `x` and `y` without using a temp variable?
19. Give an example where `set` is useful in Python.
20. Can you change the value inside a `tuple` after declaration? Why or why not?

---

## 📘 References

- [Python Official Documentation - Data Types](https://docs.python.org/3/library/stdtypes.html)
- [PEP-8 Python Style Guide](https://peps.python.org/pep-0008/)
