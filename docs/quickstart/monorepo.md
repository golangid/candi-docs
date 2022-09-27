# Generate Monorepo

Monorepo in candi's term is collection of runnable services with single .git and go.mod file.

## Init monorepo project

> After successful <a href="#/quickstart/install"> Installation </a>, open terminal inside your project and type `candi`. you will be prompted options, type `1` for monorepo and enter your `project name`.

<img src="assets/monorepo-terminal.png" />

> generated project structure :

<img src="assets/monorepo-root.png" />

## Add service to generated monorepo project

> after successfully generated then change directory to generated project by typing `cd project name` and type `candi` again to init services. type `2` to init service inside your generated monorepo project folder and type your `service name` and `module name`.

<img src="assets/monorepo-terminal-service.png" />

> generated service and module project structure :

<img src="assets/monorepo-service-module.png" />

> edit and set your database connection in `.env` file inside your service.

> **each service has its own `.env` configuration file but shared dependencies (go.mod) across other services when using monorepo project.**

> **For more detailed config <a href="#/configuration/" >Click Here</a>**

<img src="assets/monorepo-service-env.png" />

> download dependencies by typing `go mod tidy` and just type `make run service={your service name}` to run your generated service inside your monorepo project.

<img src="assets/monorepo-service-run.png" />

> **For detailed implementation <a href="#/service/module/" >Click Here</a>**