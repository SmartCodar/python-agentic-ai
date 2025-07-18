# 🔒 Understanding CORS (Cross-Origin Resource Sharing)

[![Web Security](https://img.shields.io/badge/Security-CORS-red.svg)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
[![HTTP](https://img.shields.io/badge/Protocol-HTTP-blue.svg)](https://developer.mozilla.org/en-US/docs/Web/HTTP)
[![Last Updated](https://img.shields.io/badge/Last%20Updated-July%202025-brightgreen.svg)](https://github.com/yourusername/articles)

## Table of Contents
- [Introduction](#introduction)
- [CORS Fundamentals](#cors-fundamentals)
- [CORS Headers](#cors-headers)
- [Framework Implementation](#framework-implementation)
- [Security Best Practices](#security-best-practices)
- [Troubleshooting](#troubleshooting)
- [Knowledge Check](#knowledge-check)

## Introduction

Cross-Origin Resource Sharing (CORS) is a critical security mechanism that enables controlled access to resources on different domains. This guide provides a comprehensive understanding of CORS, its implementation, and best practices for securing your web applications.

## CORS Fundamentals

### Same-Origin Policy
The same-origin policy is a fundamental browser security feature that restricts how documents and scripts on one origin can interact with resources on another origin.

**Question:** What defines a different origin?

<span style="color: #2ecc71">**Answer:**</span> An origin is considered different if any of these elements vary:
- Domain (api.example.com vs api.different.com)
- Protocol (http:// vs https://)
- Port (example.com vs example.com:8080)

### Types of CORS Requests

1. **Simple Requests**
```http
# Requirements for Simple Requests:
- Methods: GET, HEAD, POST
- Headers: Accept, Accept-Language, Content-Language, Content-Type
- Content-Types: application/x-www-form-urlencoded, multipart/form-data, text/plain
```

2. **Preflight Requests**
```http
# Triggered by:
- Methods: PUT, DELETE, PATCH
- Custom headers
- Content-Type: application/json

# Preflight OPTIONS Request
OPTIONS /api/data HTTP/1.1
Origin: https://frontend.com
Access-Control-Request-Method: PUT
Access-Control-Request-Headers: Content-Type
```

## CORS Headers

### Essential Headers
```http
# Response Headers
Access-Control-Allow-Origin: https://frontend.com
Access-Control-Allow-Methods: GET, POST, PUT, DELETE
Access-Control-Allow-Headers: Content-Type, Authorization
Access-Control-Allow-Credentials: true
Access-Control-Max-Age: 3600
```

### Header Explanations

**Question:** What is the purpose of each CORS header?

<span style="color: #2ecc71">**Answer:**</span>
```text
1. Access-Control-Allow-Origin: Specifies allowed origins
2. Access-Control-Allow-Methods: Lists permitted HTTP methods
3. Access-Control-Allow-Headers: Defines allowed custom headers
4. Access-Control-Allow-Credentials: Enables credential sharing
5. Access-Control-Max-Age: Caches preflight response time
```

## Framework Implementation

### Express.js Implementation
```javascript
const express = require('express');
const cors = require('cors');
const app = express();

// Basic CORS setup
app.use(cors({
    origin: 'https://frontend.com',
    methods: ['GET', 'POST', 'PUT', 'DELETE'],
    allowedHeaders: ['Content-Type', 'Authorization'],
    credentials: true,
    maxAge: 3600
}));

// Route-specific CORS
app.get('/api/public', cors(), (req, res) => {
    res.json({ message: 'Public API' });
});

// Custom CORS middleware
const corsOptions = (req, callback) => {
    const allowedOrigins = ['https://frontend.com', 'https://admin.frontend.com'];
    const origin = req.header('Origin');
    const isAllowed = allowedOrigins.includes(origin);
    
    callback(null, {
        origin: isAllowed,
        methods: ['GET', 'POST'],
        credentials: true
    });
};

app.get('/api/protected', cors(corsOptions), (req, res) => {
    res.json({ message: 'Protected API' });
});
```

### Flask Implementation
```python
from flask import Flask
from flask_cors import CORS

app = Flask(__name__)

# Basic CORS setup
CORS(app)

# Advanced CORS configuration
cors = CORS(app, resources={
    r"/api/*": {
        "origins": ["https://frontend.com"],
        "methods": ["GET", "POST", "PUT", "DELETE"],
        "allow_headers": ["Content-Type", "Authorization"],
        "supports_credentials": True,
        "max_age": 3600
    }
})

# Route-specific CORS
@app.route('/api/public')
@cross_origin()
def public_api():
    return {"message": "Public API"}

# Custom CORS handling
@app.route('/api/protected')
@cross_origin(origins=['https://frontend.com'], methods=['GET'])
def protected_api():
    return {"message": "Protected API"}
```

## Security Best Practices

### 1. Origin Configuration
```javascript
// ❌ Unsafe - allows all origins
Access-Control-Allow-Origin: *

// ✅ Safe - specific origin
Access-Control-Allow-Origin: https://frontend.com

// ✅ Better - dynamic validation
const allowedOrigins = ['https://frontend.com', 'https://admin.frontend.com'];
const origin = request.headers.origin;
if (allowedOrigins.includes(origin)) {
    response.setHeader('Access-Control-Allow-Origin', origin);
}
```

### 2. Credentials Handling
```javascript
// Frontend configuration
fetch('https://api.example.com/data', {
    credentials: 'include'  // Sends cookies
});

// Backend configuration
app.use(cors({
    credentials: true,
    origin: 'https://frontend.com'  // Must be specific origin, not wildcard
}));
```

### 3. Method Restrictions
```javascript
// ✅ Limit methods to what's necessary
app.use(cors({
    methods: ['GET', 'POST']  // Only allow needed methods
}));
```

## Troubleshooting

### Common CORS Errors

**Question:** How to resolve common CORS issues?

<span style="color: #2ecc71">**Answer:**</span>

1. **Invalid Origin Error**
```javascript
// Check if origin is properly configured
app.use(cors({
    origin: function(origin, callback) {
        console.log('Request from origin:', origin);
        callback(null, true);
    }
}));
```

2. **Credentials Issues**
```javascript
// Frontend
fetch(url, {
    credentials: 'include',
    headers: {
        'Content-Type': 'application/json'
    }
});

// Backend
app.use(cors({
    credentials: true,
    origin: true
}));
```

3. **Preflight Failures**
```javascript
// Add OPTIONS handling
app.options('*', cors());  // Enable preflight for all routes
```

## Knowledge Check

1. **Question:** Why is CORS necessary for web security?

<span style="color: #2ecc71">**Answer:**</span> CORS prevents malicious websites from making unauthorized requests to your API by enforcing origin restrictions at the browser level.

2. **Question:** What triggers a preflight request?

<span style="color: #2ecc71">**Answer:**</span> Preflight requests are triggered by:
- Non-simple HTTP methods (PUT, DELETE, etc.)
- Custom headers
- Complex content types (application/json)

3. **Question:** How do you handle credentials in CORS?

<span style="color: #2ecc71">**Answer:**</span> Set `Access-Control-Allow-Credentials: true` on the server and `credentials: 'include'` in fetch requests. The origin must be specifically set, not a wildcard.

4. **Question:** What's the difference between simple and preflight requests?

<span style="color: #2ecc71">**Answer:**</span> Simple requests are sent directly, while preflight requests first send an OPTIONS request to check if the actual request is allowed.

5. **Question:** How do you secure CORS in production?

<span style="color: #2ecc71">**Answer:**</span> 
- Specify exact origins instead of wildcards
- Limit allowed HTTP methods
- Carefully configure credential handling
- Implement proper validation of origins
- Use HTTPS for all communications

---

This guide covers the essential aspects of CORS implementation and security. For more detailed information, refer to the [MDN CORS documentation](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS).
