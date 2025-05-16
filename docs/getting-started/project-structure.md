# Project Structure Breakdown

This document provides an overview of the folder and file structure of a Candi-generated service. It describes the purpose and responsibility of each component to help you navigate and maintain the project.

## Root Directory

```
my-app-service/
├── cmd/
├── internal/
├── pkg/
├── server/
├── sharedmodel/
├── config/
├── docs/
├── Dockerfile
├── go.mod
├── go.sum
└── main.go
```

## Folder Responsibilities

### `cmd/`

Contains the application's entry point for starting the service. Usually contains multiple subcommands (e.g., `root.go`, `serve.go`, etc.).

### `internal/`

Core application logic, divided by domain modules.

* **Structure:**

  ```
  internal/
  ├── listing/
  │   ├── delivery/
  │   │   ├── resthandler/
  │   │   ├── grpchandler/
  │   │   └── graphqlhandler/
  │   ├── worker/
  │   │   ├── kafka_handler/
  │   │   ├── redis_subscriber/
  │   │   ├── task_queue_worker/
  │   │   ├── scheduler/
  │   │   └── postgres_event_listener/
  │   ├── repository/
  │   ├── usecase/
  │   └── model.go
  ```

* **Purpose:** Each module (e.g., `listing`) encapsulates a single business domain. It includes:

  * `delivery/`: Input handlers (e.g., HTTP, gRPC, GraphQL)
  * `worker/`: Background workers (Kafka, Redis, Task Queue, etc.)
  * `repository/`: Data access logic (DB, Redis, etc.)
  * `usecase/`: Core business logic and orchestration

### `pkg/`

Shared packages or tools that can be reused across modules (e.g., utility functions, middlewares).

### `server/`

Wires and starts various server types (REST, gRPC, GraphQL, etc.).

### `pkg/shared/domain/`

Contains struct definitions that are shared across multiple modules, such as table struct model.

### `pkg/shared/usecase/`

Contains collection of usecase shared across multiple modules.

### `pkg/shared/usecase/`

Contains collection of repository and database transaction connection shared across multiple modules.

### `config/`

Service configuration files and environment loading logic.

### `docs/`

Project documentation, including usage, development, and architectural guides.

### `Dockerfile`

Docker image definition for building and running the service.

### `go.mod` / `go.sum`

Go modules configuration.

### `main.go`

Main application entrypoint which loads the server and initiates startup logic.

---

Next: [getting-started/adding-module.md](adding-module.md?id=adding-a-new-module) - Learn how to generate a new module using the CLI.
