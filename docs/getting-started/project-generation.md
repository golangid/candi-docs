# Generate a New Project

Candi provides a CLI to quickly scaffold a clean, production-ready Go backend project. This tool helps you bootstrap with the recommended structure and optional server types (REST, gRPC, GraphQL, Kafka, Redis, etc.).

---

## Install the CLI

You can install the `candi` CLI globally using `go install`:

```bash
go install github.com/golangid/candi/cmd/candi@latest
```

After installation, run `candi --help` to see available commands.

---

## Project Generation with Candi CLI

To start generating a new project using Candi, simply run:

```bash
candi
```

You'll see a stylized welcome prompt:

```
     _____   ___   _   _______ _____ 
    /  __ \ / _ \ | \ | |  _  \_   _|
    | /  \// /_\ \|  \| | | | | | |  
    | |    |  _  || . | | | | | | |  
    | \__/\| | | || |\  | |/ / _| |_ 
     \____/\_| |_/\_| \_/___/  \___/  v1.17.0
```

Then, you will be prompted through a series of questions to generate your service.

---

## Example: Creating a New Service

Below is a step-by-step of generating a sample project with the CLI:

```
What do you want?
1) Init monorepo codebase
2) Init service
3) Add module(s) in service
4) Add delivery handler(s) in module
>> 2

[project generator]: Please input service name: 
>> my-app-service

[project generator]: Please input new module names (if more than one, separated by comma): 
>> user,order

[project generator]: Please select server handlers (separated by comma, enter for skip)
1) REST API
2) GRPC
3) GraphQL 
>> 1,2,3

[project generator]: Please select REST library (choose one, enter for default using go-chi)
1) Fiber REST API (plugin) 
>> 

[project generator]: Please select worker handlers (separated by comma, enter for skip)
1) Kafka Consumer
2) Scheduler
3) Redis Subscriber
4) Task Queue Worker
5) Postgres Event Listener Worker
6) RabbitMQ Consumer 
>> 1,2,3,4,5

[project generator]: Please select dependencies (separated by comma, enter for skip)
1) Redis
2) SQL Database
3) Mongo Database
4) Arango Database (plugin) 
>> 1,2,3

[project generator]: Please select SQL database driver (choose one)
1) Postgres
2) MySQL
3) SQLite3 
>> 1

[project generator]: Use GORM? (y/n) 
>> y

[project generator]: Use License? (y/n) 
>> n
```

---

## Generated Project Structure

After completing the prompts, a new directory `my-app-service` will be created with the following structure:

```
my-app-service/
├── api/
│   ├── graphql/
│   ├── jsonschema/
│   └── proto/
├── cmd/
│   ├── migration/
│   └── my-app-service/
├── configs/
├── deployments/k8s/
├── docs/
├── internal/modules/
│   ├── order/
│   └── user/
├── pkg/
│   ├── helper/
│   └── shared/
├── candi.json
├── go.mod
├── main.go
├── Makefile
├── Dockerfile
└── README.md
```

Each module (e.g. `user`, `order`) is scaffolded with its own:

* Delivery layer: REST, GraphQL, gRPC, and worker handlers
* Domain: request/response payloads and filters
* Repository: Mongo and SQL (if selected)
* Usecases: all CRUD logic

---

## Summary

The `candi` CLI allows you to:

* Generate new monorepo codebase / microservices with layered architecture
* Select APIs (REST/gRPC/GraphQL), workers, and DBs
* Scaffold full feature modules automatically

This helps you get up and running faster with clean, testable Go code.

---
👉 Next :
[Project Structure](getting-started/project-structure.md?id=project-structure-breakdown)


