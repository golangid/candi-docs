# Candi 

> Tired to setup every project dependencies you've just created ? [Candi](https://github.com/golangid/candi) is your answer !

## Candi Golang Framework

- **Candi is a golang framework to build golang's (microservice / monorepo) project within seconds with make file commands and easy configuration using .env file.**
- **Candi combined multiple popular golang's core framework together but not limited to add more frameworks on your own.**
- **Candi supports multiple REST handler inputs :**
  - REST API [(Echo Go Web Framework)](https://echo.labstack.com/ ':crossorgin')
  - GraphQL [(Go GraphQL)](https://github.com/graphql-go/graphql/ ':crossorgin')
  - GRPC [(Go GRPC)](https://grpc.io/docs/languages/go/quickstart/ ':crossorgin')
- **Candi supports multiple Worker handler inputs :**
  - Taskqueue Worker [(Candi's taskqueueing worker system)](https://github.com/golangid/candi/tree/master/codebase/app/task_queue_worker/ ':crossorgin')
  - Kafka Consumer / Publisher [(Sarama)](https://github.com/Shopify/sarama/ ':crossorgin')
  - Redis Subcriber / Publisher [(Go Redis)](https://github.com/go-redis/redis/ ':crossorgin')
  - RabbitMQ [(Streadway AMQP)](https://github.com/streadway/amqp ':crossorgin')
  - Scheduler [(Candi's cron worker)](https://github.com/golangid/candi/tree/master/codebase/app/cron_worker/ ':crossorgin') 
  - PostgreSQL Listner [(Go PQ with added notify event script function)](https://github.com/lib/pq/ ':crossorgin') 
- **Candi supports multiple SQL databases with / without [GORM](https://gorm.io/docs/ ':crossorgin') (golang's orm) framework :**
  - PostgreSQL
  - MySQL
  - SQLite
  - SQLServer
- **Candi supports NoSQL Databases :**
  - MongoDB
  - ArangoDB
- **Candi supports database migration using [Goose](https://github.com/pressly/goose ':crossorgin') with simplified make file command**

## Features

- **Generate code with [Uncle Bob's](https://en.wikipedia.org/wiki/Robert_C._Martin ':crossorgin') design pattern project template using simple make file commands that runs candi-cli.**
- **Low COST of RAM/CPU usage using singleton dependencies mechanism ! but still you can ruin it with your own code by the way^^**
- **Easy to add new module or just module's handler within candi's generated project using candi-cli.**
- **Candi's <i>ORIGINAL Taskqueue Worker</i> with dashboard monitoring with option to retry, stop, add new job via dashboard monitoring.**
- **[Jaeger Tracing](https://github.com/jaegertracing/jaeger-client-go/ ':crossorgin') to monitor your codes !**
- **Cross usecases among module handlers**
- **Cross data repositories among module usecases**
- **Maintanable, There is no way you can call repository layer from handlers !**
- **And many more..**

## Quick Start
<a href="#/quickstart/"> Click here to start </a>