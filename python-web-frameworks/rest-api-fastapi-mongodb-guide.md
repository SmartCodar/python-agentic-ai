# 🚀 Building Modern APIs with FastAPI and MongoDB

[![Python](https://img.shields.io/badge/Python-3.7+-blue.svg)](https://www.python.org/downloads/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.85+-orange.svg)](https://fastapi.tiangolo.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-green.svg)](https://www.mongodb.com/cloud/atlas)
[![Pydantic](https://img.shields.io/badge/Pydantic-2.0+-blue.svg)](https://pydantic-docs.helpmanual.io/)

## Table of Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Project Setup](#project-setup)
- [Pydantic Models](#pydantic-models)
- [HTTP Methods in Detail](#http-methods-in-detail)
- [MongoDB Integration](#mongodb-integration)
- [Complete CRUD Implementation](#complete-crud-implementation)
- [API Documentation](#api-documentation)
- [Error Handling](#error-handling)
- [Authentication](#authentication)
- [Best Practices](#best-practices)
- [Knowledge Check](#knowledge-check)

## Introduction

FastAPI is a modern, fast web framework for building APIs with Python 3.7+ based on standard Python type hints. This guide provides a comprehensive walkthrough of building a RESTful API with FastAPI and MongoDB, with a focus on:
- Type safety with Pydantic
- Async/await operations
- Automatic OpenAPI documentation
- MongoDB integration with Motor
- Complete CRUD operations
- Authentication and security

## Prerequisites

```bash
# Install required packages
pip install fastapi[all] motor pydantic python-dotenv uvicorn

# Create project structure
my_fastapi_project/
├── app/
│   ├── __init__.py
│   ├── main.py
│   ├── models.py
│   ├── database.py
│   └── routes/
│       └── book.py
├── .env
└── requirements.txt
```

## Project Setup

### Environment Configuration
```env
# .env
MONGODB_URL=mongodb+srv://<username>:<password>@cluster.mongodb.net/bookstore
JWT_SECRET_KEY=your_secret_key_here
```

### Database Connection
```python
# database.py
from motor.motor_asyncio import AsyncIOMotorClient
from dotenv import load_dotenv
import os

load_dotenv()

class Database:
    client: AsyncIOMotorClient = None
    
    def get_database(self):
        return self.client.bookstore
        
    async def connect_to_database(self):
        self.client = AsyncIOMotorClient(os.environ["MONGODB_URL"])
        
    async def close_database_connection(self):
        self.client.close()

db = Database()
```

## Pydantic Models

### Complete Model Definitions
```python
# models.py
from pydantic import BaseModel, Field, EmailStr
from typing import Optional, List
from datetime import datetime
from bson import ObjectId

class PyObjectId(ObjectId):
    @classmethod
    def __get_validators__(cls):
        yield cls.validate
        
    @classmethod
    def validate(cls, v):
        if not ObjectId.is_valid(v):
            raise ValueError("Invalid ObjectId")
        return ObjectId(str(v))
        
    @classmethod
    def __modify_schema__(cls, field_schema):
        field_schema.update(type="string")

class BookBase(BaseModel):
    title: str = Field(..., min_length=1, max_length=100, description="Book title")
    author: str = Field(..., min_length=1, description="Book author")
    description: Optional[str] = Field(None, max_length=1000)
    price: float = Field(..., gt=0, description="Book price")
    stock: int = Field(..., ge=0, description="Books in stock")
    genres: List[str] = Field(default_factory=list)
    published_year: Optional[int] = Field(None, gt=1000, lt=datetime.now().year + 1)
    
    class Config:
        schema_extra = {
            "example": {
                "title": "The Great Gatsby",
                "author": "F. Scott Fitzgerald",
                "description": "A story of the fabulously wealthy Jay Gatsby",
                "price": 9.99,
                "stock": 50,
                "genres": ["Fiction", "Classic"],
                "published_year": 1925
            }
        }

class BookCreate(BookBase):
    pass

class BookUpdate(BaseModel):
    title: Optional[str] = Field(None, min_length=1, max_length=100)
    author: Optional[str] = Field(None, min_length=1)
    description: Optional[str] = None
    price: Optional[float] = Field(None, gt=0)
    stock: Optional[int] = Field(None, ge=0)
    genres: Optional[List[str]] = None
    published_year: Optional[int] = None

class Book(BookBase):
    id: PyObjectId = Field(default_factory=PyObjectId, alias="_id")
    created_at: datetime = Field(default_factory=datetime.utcnow)
    updated_at: Optional[datetime] = None
    
    class Config:
        allow_population_by_field_name = True
        arbitrary_types_allowed = True
        json_encoders = {ObjectId: str}
```

## HTTP Methods in Detail

### Complete CRUD Implementation
```python
# routes/book.py
from fastapi import APIRouter, HTTPException, Depends, Query, Path
from typing import List, Optional
from ..models import Book, BookCreate, BookUpdate
from ..database import db
from bson import ObjectId
from datetime import datetime

router = APIRouter()

# CREATE - POST Method
@router.post("/", response_model=Book, status_code=201)
async def create_book(book: BookCreate):
    """
    Create a new book with the following information:
    - **title**: required, book title
    - **author**: required, book author
    - **price**: required, must be greater than 0
    - **stock**: required, must be 0 or positive
    - **genres**: optional list of genres
    - **published_year**: optional publication year
    """
    book_dict = book.dict()
    book_dict["created_at"] = datetime.utcnow()
    
    try:
        new_book = await db.get_database().books.insert_one(book_dict)
        created_book = await db.get_database().books.find_one(
            {"_id": new_book.inserted_id}
        )
        return created_book
    except Exception as e:
        raise HTTPException(status_code=400, detail=str(e))
```

### PUT Method

```python
@app.put("/books/{book_id}", response_model=Book)
async def update_book(book_id: str, book: BookCreate):
    update_result = await app.mongodb.books.update_one(
        {"_id": book_id}, {"$set": book.dict()}
    )
    
    if update_result.modified_count == 0:
        raise HTTPException(status_code=404, detail=f"Book {book_id} not found")
        
    return await app.mongodb.books.find_one({"_id": book_id})
```

### DELETE Method

```python
@app.delete("/books/{book_id}")
async def delete_book(book_id: str):
    delete_result = await app.mongodb.books.delete_one({"_id": book_id})
    
    if delete_result.deleted_count == 0:
        raise HTTPException(status_code=404, detail=f"Book {book_id} not found")
        
    return {"message": "Book deleted successfully"}
```

## MongoDB Integration

### Async MongoDB Setup with Motor

```python
# config.py
from motor.motor_asyncio import AsyncIOMotorClient
from dotenv import load_dotenv
import os

load_dotenv()

class MongoDBSettings:
    MONGODB_URL: str = os.getenv("MONGODB_URL", "mongodb://localhost:27017")
    DB_NAME: str = "bookstore"

async def get_mongodb():
    client = AsyncIOMotorClient(MongoDBSettings.MONGODB_URL)
    try:
        yield client[MongoDBSettings.DB_NAME]
    finally:
        client.close()
```

### Advanced Queries

```python
# Complex query examples
@app.get("/books/search")
async def search_books(
    author: Optional[str] = None,
    year: Optional[int] = None,
    genre: Optional[str] = None,
    skip: int = 0,
    limit: int = 10
):
    query = {}
    if author:
        query["author"] = {"$regex": author, "$options": "i"}
    if year:
        query["year"] = year
    if genre:
        query["genres"] = genre
        
    cursor = app.mongodb.books.find(query).skip(skip).limit(limit)
    books = await cursor.to_list(length=limit)
    
    total = await app.mongodb.books.count_documents(query)
    
    return {
        "total": total,
        "books": books,
        "page": skip // limit + 1,
        "pages": (total + limit - 1) // limit
    }
```

## Data Validation with Pydantic

### Model Definitions

```python
from pydantic import BaseModel, Field
from typing import Optional, List
from datetime import datetime

class BookBase(BaseModel):
    title: str = Field(..., min_length=1, max_length=100)
    author: str = Field(..., min_length=1, max_length=50)
    year: Optional[int] = Field(None, gt=1000, lt=datetime.now().year + 1)
    genres: List[str] = Field(default_factory=list)
    
    class Config:
        schema_extra = {
            "example": {
                "title": "The Great Gatsby",
                "author": "F. Scott Fitzgerald",
                "year": 1925,
                "genres": ["Novel", "Fiction"]
            }
        }

class BookCreate(BookBase):
    pass

class Book(BookBase):
    id: str = Field(..., alias="_id")
    created_at: datetime = Field(default_factory=datetime.utcnow)
    updated_at: Optional[datetime] = None
    
    class Config:
        allow_population_by_field_name = True
```

## Error Handling

### Custom Exception Handler

```python
from fastapi import FastAPI, Request, status
from fastapi.responses import JSONResponse

class BookException(Exception):
    def __init__(self, status_code: int, detail: str):
        self.status_code = status_code
        self.detail = detail

@app.exception_handler(BookException)
async def book_exception_handler(request: Request, exc: BookException):
    return JSONResponse(
        status_code=exc.status_code,
        content={"detail": exc.detail}
    )

# Usage in endpoints
@app.get("/books/{book_id}")
async def get_book(book_id: str):
    if not await app.mongodb.books.find_one({"_id": book_id}):
        raise BookException(
            status_code=status.HTTP_404_NOT_FOUND,
            detail=f"Book {book_id} not found"
        )
```

## Best Practices

### Rate Limiting

```python
from fastapi import FastAPI, Request
from fastapi.middleware.cors import CORSMiddleware
from slowapi import Limiter, _rate_limit_exceeded_handler
from slowapi.util import get_remote_address
from slowapi.errors import RateLimitExceeded

limiter = Limiter(key_func=get_remote_address)
app = FastAPI()
app.state.limiter = limiter
app.add_exception_handler(RateLimitExceeded, _rate_limit_exceeded_handler)

@app.get("/books")
@limiter.limit("10/minute")
async def get_books(request: Request):
    # Implementation
    pass
```

### Request Logging Middleware

```python
import time
from fastapi import FastAPI, Request
from fastapi.middleware.base import BaseHTTPMiddleware
import logging

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

class LoggingMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request: Request, call_next):
        start_time = time.time()
        response = await call_next(request)
        process_time = time.time() - start_time
        logger.info(f"{request.method} {request.url.path} {response.status_code} {process_time:.4f}s")
        return response

app.add_middleware(LoggingMiddleware)
```

## Knowledge Check

1. **Question:** What are the key differences between FastAPI and Flask?
   **Answer:** FastAPI offers built-in async support, automatic OpenAPI documentation, data validation with Pydantic, and better performance through Starlette and Uvicorn.

2. **Question:** How does FastAPI handle request validation?
   **Answer:** FastAPI uses Pydantic models for automatic request/response validation, type checking, and documentation generation.

3. **Question:** Explain async/await in FastAPI.
   **Answer:** FastAPI uses Python's async/await for non-blocking I/O operations, allowing multiple requests to be handled concurrently without blocking the event loop.

4. **Question:** How do you handle CORS in FastAPI?
   **Answer:** Use CORSMiddleware with specific origins, methods, and headers:
   ```python
   app.add_middleware(
       CORSMiddleware,
       allow_origins=["*"],
       allow_methods=["*"],
       allow_headers=["*"]
   )
   ```

5. **Question:** How do you implement pagination in FastAPI with MongoDB?
   **Answer:** Use skip and limit parameters with Motor's find() method, returning total count and page information in the response.

---

This guide provides a solid foundation for building modern APIs with FastAPI and MongoDB. For more advanced topics and detailed examples, refer to the official FastAPI documentation.
