# 📝 Application Logging in Python – Guide for Developers

Logging is one of the most critical components of modern applications. Whether you're building a FastAPI service, handling AWS jobs, or managing background tasks, logs provide visibility, diagnostics, and audit trails essential for debugging and monitoring.

---

## 🔍 1. What is Logging?

Logging refers to the process of recording events, messages, and runtime information of an application. It helps you:

- Track application behavior in production
- Debug issues in development
- Audit events for security and compliance
- Monitor performance and user actions

---

## 🪵 2. Logging Levels in Python

Python’s `logging` module has five standard log levels:

| Level      | Purpose                                                             |
|------------|----------------------------------------------------------------------|
| `DEBUG`    | Detailed info for diagnosing problems (dev only)                    |
| `INFO`     | General operational entries (e.g., app started, user logged in)     |
| `WARNING`  | Unexpected events, but app still works                              |
| `ERROR`    | Errors that affect operation, but not crashing                      |
| `CRITICAL` | Severe errors likely to crash or halt service                       |

### Example:
```python
import logging

logging.basicConfig(level=logging.DEBUG)
logging.debug("This is a debug message for dev diagnostics")
logging.info("User successfully logged in")
logging.warning("Disk usage nearing 90%")
logging.error("Database connection failed")
logging.critical("System out of memory")
```

---

## 🛠️ 3. Basic Logging Setup

```python
import logging

logging.basicConfig(
    filename="app.log",
    level=logging.INFO,
    format="%(asctime)s - %(levelname)s - %(message)s"
)

logging.info("App started")
```

- `filename`: Logs will be saved to `app.log`
- `level`: Minimum log level to capture
- `format`: Custom format for each line

---

## 📄 4. Log Format Options

### Default format:
```python
'%(levelname)s:%(message)s'
```

### Timestamped format:
```python
'%(asctime)s - %(levelname)s - %(message)s'
```

### With module and line number:
```python
'%(asctime)s - %(levelname)s - %(name)s - Line:%(lineno)d - %(message)s'
```

### JSON-style logging:
```python
import json, logging

logging.basicConfig(level=logging.INFO)

def log_json(event, level="INFO"):
    print(json.dumps({"event": event, "level": level}))

log_json("user_registered", "INFO")
```

---

## 📦 5. Storing Logs

| Location        | Use Case                       |
|----------------|---------------------------------|
| Local File      | Traditional apps, debugging    |
| stdout / stderr | Dockerized apps, cloud-native  |
| AWS CloudWatch  | Production cloud logs           |
| ELK Stack       | Log analysis at scale          |

---

## 🔁 6. Rotating and Archiving Logs

```python
from logging.handlers import RotatingFileHandler

handler = RotatingFileHandler("logfile.log", maxBytes=200000, backupCount=5)
logging.basicConfig(handlers=[handler], level=logging.INFO)
```

✅ Automatically rotates logs when size exceeds 200KB, keeps 5 backups.

---

## ⚙️ 7. Advanced Config with `dictConfig`

```python
import logging.config

LOG_CONFIG = {
    "version": 1,
    "formatters": {
        "default": {
            "format": "%(asctime)s - %(name)s - %(levelname)s - %(message)s"
        }
    },
    "handlers": {
        "console": {
            "class": "logging.StreamHandler",
            "formatter": "default"
        }
    },
    "root": {
        "handlers": ["console"],
        "level": "DEBUG"
    }
}

logging.config.dictConfig(LOG_CONFIG)
logging.debug("Advanced config logging")
```

---

## 🧪 8. Logging with Context

### Log with metadata:
```python
logger = logging.getLogger("logfile.app")
logger.info("Job completed", extra={"job_id": "ABC123"})
```

---

## 🔥 9. Exception Logging

```python
try:
    1 / 0
except ZeroDivisionError as e:
    logging.exception("ZeroDivisionError occurred")
```

✅ Logs the full traceback with `ERROR` level.

---

## 🛡️ 10. Best Practices

- Use `DEBUG` in dev, `INFO/WARNING` in prod
- Don’t log secrets (passwords, tokens)
- Use structured logging for services
- Always rotate and clean old logs

---

## 📚 11. Quiz – Logging Knowledge Check (20 Questions)

| # | Question |
|--:|:---------|
| 1 | What’s the default log level in Python if not set? |
| 2 | Which log level should you avoid in production? |
| 3 | How do you format log messages with timestamps? |
| 4 | What does `RotatingFileHandler` do? |
| 5 | How do you log to both console and file at once? |
| 6 | How to capture full exception stack in logs? |
| 7 | When would you use `logger.debug()`? |
| 8 | What log level is best for user signup events? |
| 9 | What is `dictConfig` used for? |
| 10 | Can logging capture line numbers automatically? |
| 11 | What’s the benefit of structured JSON logs? |
| 12 | Where are logs sent in Docker containers by default? |
| 13 | What’s the use of `extra` in logger.info()? |
| 14 | How do you clear/rotate logs older than X days? |
| 15 | What’s the difference between `logger.error()` and `logger.exception()`? |
| 16 | How do you prevent logging sensitive data? |
| 17 | Why is log level control important between dev and prod? |
| 18 | How do you handle multi-file logs in microservices? |
| 19 | How to tag logs per job/user? |
| 20 | What Python function initializes basic logging setup? |

---
