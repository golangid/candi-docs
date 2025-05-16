# Adding a New Handler to an Existing Module

This guide shows how to add a new delivery or worker handler to an already existing module using the Candi CLI.

## Step-by-Step CLI Guide

From your service directory, run:

```bash
cd ~/Documents/codes/my-app/my-app-service
candi
```

Candi CLI will start:

```
What do you want?
1) Init monorepo codebase
2) Init service
3) Add module(s) in service
4) Add delivery handler(s) in module
>> 4
```

### 1. Choose Option `4`: Add delivery handler(s) in module

```
[project generator]: Please input existing module name to be added delivery handler(s):
>> listing
```

Input the module name exactly as it exists in the `internal/` folder.

### 2. Select Worker Handlers to Add

```
[project generator]: Please select worker handlers (separated by comma, enter for skip)
1) RabbitMQ Consumer
>> 1
```

Candi will add boilerplate for the selected handler(s) inside the specified module:

```
internal/
└── listing/
    └── worker/
        └── rabbitmq_consumer/
            ├── handler.go
            └── consumer.go
```

## Notes

* You can re-run this process multiple times to add more handlers.
* The CLI is non-destructive: existing logic will not be overwritten.

---

Next: Explore [project-structure.md](project-structure.md) to understand the full layout of your Candi-generated service.
