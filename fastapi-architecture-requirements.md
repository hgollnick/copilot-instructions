# 🧑‍💻 FastAPI Project Requirements and Architecture Guidelines

This document outlines the best practices and design requirements to structure and maintain a scalable, testable, and maintainable FastAPI project.

---

## 📁 Folder Structure

Organize your FastAPI project using a **modular architecture**, separating concerns into well-defined layers.

```
myapp/
│
├── app/                    # Main application package
│   ├── api/                # API layer (routes/controllers)
│   │   ├── v1/             # Versioned APIs
│   │   │   ├── endpoints/  # Specific route files
│   │   │   │   └── users.py
│   │   │   └── __init__.py
│   │   └── __init__.py
│   │
│   ├── core/               # Application-specific settings/configs
│   │   └── config.py       # Env, secrets, and app settings
│   │
│   ├── models/             # Pydantic and ORM models
│   │   ├── user.py
│   │   └── __init__.py
│   │
│   ├── schemas/            # Request and response schemas (DTOs)
│   │   ├── user.py
│   │   └── __init__.py
│   │
│   ├── services/           # Business logic layer (aka use cases)
│   │   ├── user_service.py
│   │   └── __init__.py
│   │
│   ├── repositories/       # Database access logic
│   │   ├── user_repository.py
│   │   └── __init__.py
│   │
│   ├── db/                 # Database initialization and session
│   │   ├── base.py         # SQLAlchemy base
│   │   ├── session.py      # DB session handling
│   │   └── init_db.py
│   │
│   ├── main.py             # Application entrypoint
│   └── dependencies.py     # Shared dependencies (e.g. get_db)
│
├── tests/                  # Test suite
│   ├── unit/
```