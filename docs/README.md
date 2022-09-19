# Candi  <!-- {docsify-ignore} -->

> Tired to setup every project dependencies you've just created ? Or you just signed to a company and trying to add new module but too hard to trace almost the whole code from main.go just to know how to inject the dependencies ? Candi is your answer !

# Candi Golang Framework

<p align="center">
  <img src="https://storage.googleapis.com/agungdp/static/logo/golang.png" width="80" alt="golang logo" />
  <img src="https://storage.googleapis.com/agungdp/static/logo/docker.png" width="80" hspace="10" alt="docker logo" />
  <img src="https://storage.googleapis.com/agungdp/static/logo/rest.png" width="80" hspace="10" alt="rest logo" />
  <img src="https://storage.googleapis.com/agungdp/static/logo/graphql.png" width="80" alt="graphql logo" />
  <img src="https://storage.googleapis.com/agungdp/static/logo/grpc.png" width="160" hspace="15" vspace="15" alt="grpc logo" />
  <img src="https://storage.googleapis.com/agungdp/static/logo/kafka.png" height="80" alt="kafka logo" />
</p>



- **Candi is a golang framework to build golang's (microservice / monorepo) project within seconds with make file commands and easy configuration using .env file.**
- **Candi combined multiple popular golang's core framework together but not limited to add more frameworks on your own.**
- **Candi supports multiple REST handler inputs :**
  - REST API
  - GraphQL
  - GRPC
- **Candi supports multiple Worker handler inputs :**
  - Taskqueue Worker (Candi's original taskqueueing worker system)
  - Kafka Consumer / Publisher
  - Redis Subcriber / Publisher
  - RabbitMQ
  - Scheduler
  - PostgreSQL Listner
- **Candi supports multiple SQL databases with / without gorm (golang's orm) framework :**
  - PostgreSQL
  - MySQL
  - SQLite
  - SQLServer
- **Candi supports NoSQL Databases :**
  - MongoDB, ArangoDB.

# Features

- **Generate code with Uncle Bob's Pattern project template using simple make file commands that runs candi-cli.**
- **Low COST of RAM/CPU usage using singleton dependencies mechanism ! but still you can ruin it with your own code by the way^^**
- **Easy to add new module or just module's handler within candi's generated project using candi-cli.**
- **Candi's <i>ORIGINAL Taskqueue Worker</i> with dashboard monitoring with option to retry, stop, add new job via dashboard monitoring.**
- **Jaeger tracing monitoring to monitor your codes !**
- **Cross usecases among handlers**
- **Cross data repositories among usecases**
- **Maintanable, There is no way you can call repository layer from handlers !**
