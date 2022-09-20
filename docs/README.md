# Candi <!-- {docsify-ignore-all} -->

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

# Features

- **Generate code with [Uncle Bob's](https://en.wikipedia.org/wiki/Robert_C._Martin ':crossorgin') design pattern project template using simple make file commands that runs candi-cli.**
- **Low COST of RAM/CPU usage using singleton dependencies mechanism ! but still you can ruin it with your own code by the way^^**
- **Easy to add new module or just module's handler within candi's generated project using candi-cli.**
- **Candi's <i>ORIGINAL Taskqueue Worker</i> with dashboard monitoring with option to retry, stop, add new job via dashboard monitoring.**
- **[Jaeger Tracing](https://github.com/jaegertracing/jaeger-client-go/ ':crossorgin') to monitor your codes !**
- **Cross usecases among module handlers**
- **Cross data repositories among module usecases**
- **Maintanable, There is no way you can call repository layer from handlers !**
- **And many more..** <a href="#/quickstart/"> Click here to start </a>

