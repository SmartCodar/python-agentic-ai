
# ✅ Python Guide to HTTP Methods, API Requests & Postman

## 📖 Introduction

In modern web development, **HTTP methods** and **API requests** are the backbone of client-server communication. This guide explains **GET, POST, PUT, PATCH, DELETE**, path/query parameters, request bodies, and how to use **Postman** and **Python** for API testing.

---

## 🎯 HTTP Methods Overview

| Method   | Purpose                                  | Example Use Case                          |
|-----------|------------------------------------------|--------------------------------------------|
| GET       | Retrieve data                           | Fetch user details                         |
| POST      | Create new resource                     | Register a new user                        |
| PUT       | Update/Replace resource                 | Replace entire user profile                |
| PATCH     | Partial update of resource              | Update only user's email address           |
| DELETE    | Delete a resource                       | Remove a user account                      |
| OPTIONS   | Check allowed methods                   | Preflight request in browsers              |
| HEAD      | Retrieve headers only                   | Check file metadata without downloading    |

---

## 📊 REST API Components

| Component           | Explanation                                         | Example                                              |
|----------------------|-----------------------------------------------------|-------------------------------------------------------|
| Path Parameters      | Identifiers in the endpoint path                    | `/users/{id}` → `/users/101`                          |
| Query Parameters     | Filters after `?`                                   | `/products?category=books&price=100`                  |
| Request Body         | Data sent in POST/PUT/PATCH requests (JSON)          | `{ "name": "Amit", "email": "amit@example.com" }`     |
| Headers              | Meta info like Auth Tokens, Content-Type            | `Authorization: Bearer TOKEN`, `Content-Type: json`   |

---

## 🧪 Python Code Examples with `requests`

### ✅ GET Request with Query Params

```python
import requests

response = requests.get("https://jsonplaceholder.typicode.com/posts", params={"userId": 1})
print(response.json())
```

### ✅ POST Request with JSON Body

```python
data = {"title": "New Post", "body": "Learning API", "userId": 1}
response = requests.post("https://jsonplaceholder.typicode.com/posts", json=data)
print(response.status_code, response.json())
```

### ✅ PUT Request (Full Update)

```python
url = "https://jsonplaceholder.typicode.com/posts/1"
data = {"id": 1, "title": "Updated", "body": "Updated Content", "userId": 1}
response = requests.put(url, json=data)
print(response.json())
```

### ✅ PATCH Request (Partial Update)

```python
response = requests.patch("https://jsonplaceholder.typicode.com/posts/1", json={"title": "Patched Title"})
print(response.json())
```

### ✅ DELETE Request

```python
response = requests.delete("https://jsonplaceholder.typicode.com/posts/1")
print(response.status_code)  # 200 means deleted
```

---

## 🛠️ Using Postman

- **Create Collection** for organized requests.
- Use **Authorization tab** to manage tokens (Bearer, Basic Auth).
- Add **Query Params** under the Params section.
- Set **Request Body** (raw JSON) in the Body tab.
- **Save responses** and **generate code snippets** (Python/NodeJS).

---

## 🧾 Common HTTP Error Codes

| Status Code | Meaning                        | Description                                       |
|--------------|---------------------------------|---------------------------------------------------|
| 200          | OK                              | Request successful                                |
| 201          | Created                         | Resource successfully created                     |
| 204          | No Content                      | Request successful, no response body              |
| 400          | Bad Request                     | Invalid input from client                         |
| 401          | Unauthorized                    | Missing or invalid authentication                 |
| 403          | Forbidden                       | Authenticated but not authorized                  |
| 404          | Not Found                       | Requested resource doesn't exist                  |
| 405          | Method Not Allowed              | Method not allowed on the requested resource      |
| 409          | Conflict                        | Resource conflict (e.g., duplicate record)        |
| 500          | Internal Server Error           | Server encountered an error                       |
| 502          | Bad Gateway                     | Invalid response from upstream server             |
| 503          | Service Unavailable             | Server temporarily unavailable or overloaded      |

---

## 🎓 requests vs Postman

| Feature               | Python (`requests`)                  | Postman                                  |
|------------------------|---------------------------------------|-------------------------------------------|
| Automation             | Ideal for scripts & batch requests   | Manual request execution                  |
| UI                     | CLI-based                            | Graphical Interface                        |
| Testing Collections    | Programmatic loops & functions       | Pre-configured collections & environments  |
| Multi-Step Workflow    | Custom logic via code                | Pre/Post request scripts supported         |

---

## 🧠 Summary

- **GET** = Read, **POST** = Create, **PUT/PATCH** = Update, **DELETE** = Remove.
- Use **Path Params** for direct identifiers, **Query Params** for filters.
- Use **Body** to send data in POST/PUT/PATCH.
- **Postman** is useful for interactive testing; **requests** for automation.

---

## 🔍 Quiz Time

1. Which HTTP method is used to **retrieve data**?
2. Which method is **idempotent** between POST and PUT?
3. How do you pass **query parameters** in a Python requests GET call?
4. When should you use **PATCH** instead of PUT?
5. Which method is used to **delete a resource**?
6. What is the difference between **path params** and **query params**?
7. How do you **send JSON data** in a POST request using Python?
8. Which Postman section is used to send a **Bearer Token**?
9. Which method would you use to **upload a new blog post**?
10. How do you **check allowed methods** on an API?
11. Explain the purpose of the **HEAD** method.
12. Which **status code** typically indicates **successful DELETE**?
13. How can you automate **multiple API calls** in Python?
14. Where do you define **request headers** in Postman?
15. Difference between **PATCH** and **PUT**?
16. What’s the purpose of **OPTIONS** request in APIs?
17. How to handle **timeout errors** in Python requests?
18. Which method can be **cached** safely - GET or POST?
19. Which data structure is used to **pass headers** in Python requests?
20. How to **simulate POST request** in Postman and **generate code snippet**?

---

## 📘 References

- [Python requests Docs](https://docs.python-requests.org/en/latest/)
- [Postman API Testing Docs](https://learning.postman.com/docs/getting-started/introduction/)
- [REST API Tutorial](https://restfulapi.net/)
