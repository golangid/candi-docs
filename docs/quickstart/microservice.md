# Generate Microservice

Microservice in candi's term is single runable service with single .git and go.mod file.

### Init microservice project

> After successful <a href="#/quickstart/install"> Installation </a>

1. Open terminal inside your project / empty cloned git repository and type `candi`. 
2. Choose `init service` by entering number of init service.
3. Enter your `service name`.
4. Enter your `module name`.
5. Choose your API server handler, enter blank to skip API handler. separate with commas for multiple API handlers.
6. Choose your Worker server handler, enter blank to skip Worker handler. separate with commas for multiple Worker handlers.
7. Choose your database dependencies. separate with commas for multiple database dependencies.
8. Choose your SQL Driver.

<img src="assets/microservice-terminal.png" />

> Your generated project structure will look like this

**Note : you can delete cmd/migration/`xxxxxxxx_create_table_{module_name}.sql` migration file. for more information of database migration <a href="#/migration/"> Click Here </a>**

<img src="assets/microservice-structure.png" />

### Run generated microservice project

1. to run you need to edit and set your database connection in `.env` file inside your service. **For more detailed config <a href="#/configuration/" >Click Here</a>**
2. download dependencies by typing `go mod tidy` and just type `make run` to run your generated microservice.

<img src="assets/microservice-run.png" />

> **For detailed implementation <a href="#/service/module/" >Click Here</a>**