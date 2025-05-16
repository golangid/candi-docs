# Adding a New Module

This guide explains how to generate a new module in an existing Candi service.

## Step-by-Step CLI Guide

Open a terminal and navigate to your service root:

```bash
cd ~/Documents/codes/my-app/my-app-service
candi
```

You'll see the Candi CLI welcome banner:

```
What do you want?
1) Init monorepo codebase
2) Init service
3) Add module(s) in service
4) Add delivery handler(s) in module
>> 3
```

### 1. Choose Option `3`: Add module(s) in service

```
[project generator]: Please input new module names (if more than one, separated by comma):
>> listing
```

You can input multiple module names, separated by commas (e.g., `listing, user, cart`).

### 2. Select Server Handlers

Candi will prompt you to choose server delivery types:

```
[project generator]: Please select server handlers (separated by comma, enter for skip)
1) REST API
2) GRPC
3) GraphQL
>> 1,2,3
```

Choose the ones needed for your module. These handlers will be scaffolded automatically inside the module under `delivery/`.

### 3. Select Worker Handlers

Candi will then prompt for worker-based delivery types:

```
[project generator]: Please select worker handlers (separated by comma, enter for skip)
1) Kafka Consumer
2) Scheduler
3) Redis Subscriber
4) Task Queue Worker
5) Postgres Event Listener Worker
6) RabbitMQ Consumer
>> 1,2,3,4,5
```

These will be scaffolded in the module under the `worker/` directory.

## Resulting Structure

Your module folder will be created under `internal/<module_name>/`, e.g.:

```
internal/
└── listing/
    ├── delivery/
    ├── worker/
    ├── repository/
    ├── usecase/
    └── model.go
```

Each selected handler will have its boilerplate ready.

---

Next: [getting-started/adding-handler.md](adding-handler.md?id=adding-a-new-handler-to-an-existing-module) - Learn how to add a handler to an existing module.
