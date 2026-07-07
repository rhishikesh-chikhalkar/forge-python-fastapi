# Domain Layer

This package contains **pure business logic** — the core rules and entities
that define what the application *does*, independent of how it's deployed
or what frameworks it uses.

## Rules

1. **No framework imports** — no FastAPI, SQLAlchemy, Celery, or HTTP concepts.
   If you need to import from `fastapi`, `sqlalchemy`, or any infrastructure
   package, the code belongs in `services/`, `repositories/`, or `views/` instead.

2. **No I/O** — domain code must not read files, call APIs, or touch databases
   directly. All external data flows through repository interfaces.

3. **Pure functions preferred** — stateless functions are easier to test and
   reason about. Use dataclasses or Pydantic models for value objects.

4. **Business exceptions** — define domain-specific exception classes here
   (e.g., `InsufficientBalance`, `OrderAlreadyShipped`) rather than using
   generic HTTP errors.

## Example structure

```
domain/
├── __init__.py
├── entities/
│   ├── user.py          # User value object / entity
│   └── order.py         # Order entity with business rules
├── exceptions.py        # Domain-specific exceptions
└── value_objects/
    └── money.py         # Money value object with currency math
```
