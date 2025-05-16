# What is Candi?

**Candi** is a **Go (Golang) backend framework and project generator** designed for building scalable, modular, and production-ready backend services with **Clean Architecture** principles.

---

## Key Features

* **Clean Architecture** by default (separation of concerns: handler, usecase, repository)
* **Project Generator CLI** for rapid scaffolding
* Support for multiple **server types**:

  * REST API (HTTP)
  * GraphQL
  * gRPC
  * Kafka Consumer
  * Redis Subscriber
  * PostgreSQL Event Listener
* Background worker support: task queue, scheduler, job retries
* Built-in middleware support (auth, logger, metrics, etc.)
* Easier testing due to clear separation of logic and interfaces

---

## Architecture Overview

Candi uses **Clean Architecture** to enforce:

* Dependency inversion (business logic doesn't depend on infrastructure)
* Maintainability and testability
* Consistent patterns across services

The standard layers:

```
Delivery (REST/gRPC/GraphQL) → Usecase → Repository
```

Each module (feature) is **self-contained**, enabling easy scaling and collaboration.

* candi share usecases and repositories between modules.
* shared repositories responsible to maintain transaction between module's repositories.

sample case of shared usecases :
```
→ Module's Delivery requires authentication middleware and permission to access API
→ Check user's id from JWT token
→ Check user's permissions from database which require usecase to access database
```

sample case of shared repositories :
```
→ Create a data which required to save into different modules.
→ Usecase A will Call Repository A, Repository B, etc.
```

---

## When Should You Use Candi?

Use Candi if:

* You want to build a **scalable backend service** in Go
* You prefer **Clean Architecture** or need better modularization
* You want support for **multiple protocols** (e.g., REST, Kafka, GraphQL) in one service
* You're building microservices and need clean separation for each feature

---

## Summary

Candi is ideal for teams and developers looking to **standardize Go microservices**, enforce good architecture, and support multiple server protocols in a unified, testable way.


---

👉 Lets Start Here

[Generate Your Project](getting-started/project-generation.md?id=generate-a-new-project)

---

For full source code and contribution, visit the [Candi GitHub repository](https://github.com/golangid/candi).
