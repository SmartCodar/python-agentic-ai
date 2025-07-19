# ✅ Masterclass - All about Python Decorators with Real-World Examples

## What is a Decorator?

A **decorator** in Python is a higher-order function that wraps another function to **extend or modify** its behavior **without changing the original function's code**.

This is useful in real-world applications such as:
- Logging
- Authentication
- Access control
- Execution timing
- Retry mechanisms
- Data validation

---

## 🎯 Syntax Overview

```python
def decorator_function(original_function):
    def wrapper_function(*args, **kwargs):
        # Pre-processing
        result = original_function(*args, **kwargs)
        # Post-processing
        return result
    return wrapper_function
```

Usage:

```python
@decorator_function
def target_function():
    pass
```

---

## ✅ Basic Decorator Example 

```python
def log_action(func):
    def wrapper(*args, **kwargs):
        print(f"[LOG] Executing: {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

@log_action
def enroll_user(name):
    print(f"{name} has been enrolled successfully.")

enroll_user("Amitabh")
```

---

## 🧪 Decorator with Arguments

```python
def notify(admin):
    def decorator(func):
        def wrapper(*args, **kwargs):
            print(f"Notify {admin} before executing {func.__name__}")
            return func(*args, **kwargs)
        return wrapper
    return decorator

@notify("ameet@chocosoft.in")
def approve_application(name):
    print(f"{name}'s application has been approved.")

approve_application("Rajeev")
```

---

## ⏱️ Timing Decorator

```python
import time

def timing(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} took {end - start:.4f} seconds")
        return result
    return wrapper

@timing
def process_data():
    time.sleep(2)
    print("Processing data...")

process_data()
```

---

## 🔁 Retry Decorator

```python
import random

def retry(max_attempts):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for attempt in range(max_attempts):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    print(f"Attempt {attempt + 1} failed: {e}")
            print("All retries failed.")
        return wrapper
    return decorator

@retry(3)
def connect_to_service():
    if random.random() < 0.7:
        raise ConnectionError("Service unavailable")
    return "Connected successfully!"

print(connect_to_service())
```

---

## 🛡️ Access Control Decorator (Indian Names & Roles)

```python
def require_role(role):
    def decorator(func):
        def wrapper(user):
            if user.get("role") == role:
                return func(user)
            else:
                print(f"Access Denied for {user['name']}. Required: {role}")
        return wrapper
    return decorator

@require_role("manager")
def view_team_performance(user):
    print(f"Manager {user['name']} is viewing team dashboard.")

user1 = {"name": "Sundar", "role": "manager"}
user2 = {"name": "Deepa", "role": "analyst"}

view_team_performance(user1)  # ✅
view_team_performance(user2)  # ❌
```

---

## 🎓 Real-World Use Cases in Zennial Pro

| Use Case                     | Decorator Name      | Description                                      |
|------------------------------|---------------------|--------------------------------------------------|
| Audit Log                    | `@log_action`       | Track all admin actions                          |
| Time Monitoring              | `@timing`           | Measure time for training module processing      |
| Retry Upload                 | `@retry(3)`         | Retry file uploads to S3 if network fails        |
| User Role Verification       | `@require_role('HR')` | Ensure access is restricted based on role       |
| Email Notification           | `@notify(admin)`    | Auto-notify admins on workflow triggers          |

---

## 🧠 Summary

- Decorators wrap functions to transparently extend behavior
- You can use them for logging, timing, retries, auth, etc.
- Use `functools.wraps` to preserve metadata (e.g. `__name__`)
- Common in frameworks like Flask, FastAPI, Django, etc.

---

## 🔍 Quiz Time

1. What’s the benefit of using a decorator over manually adding code to each function?
2. How do you create a decorator that accepts arguments (like `@retry(3)`)?
3. In which real-world case would you use a `@require_role` decorator?
4. Can decorators be stacked? What is the order of execution?
5. What is the difference between a function and a decorator function?
6. How can you preserve the metadata of a function while using a decorator?
7. What module provides `@wraps` to preserve function name and docstring?
8. How would you time the execution of a function using a decorator?
9. Write a decorator that logs input arguments and return value of a function.
10. Can a decorator modify the return value of the original function?
11. How do you create a decorator that can be applied to both sync and async functions?
12. What’s the use of `*args` and `**kwargs` in decorators?
13. Explain the difference between class-based and function-based decorators.
14. Can a decorator be used to handle exceptions in a function? Give an example.
15. How do you implement caching (memoization) using a decorator?
16. What happens if a decorator is applied to a method instead of a function?
17. What’s the purpose of using decorators in frameworks like FastAPI or Flask?
18. Is it possible to remove or disable a decorator at runtime? Why or why not?
19. Can decorators be used to enforce authentication in APIs?
20. Why should decorators always return a callable?

---

## 📘 References

- [Python Docs – Decorators](https://docs.python.org/3/glossary.html#term-decorator)
- [Real Python – Primer on Python Decorators](https://realpython.com/primer-on-python-decorators/)