# subject: [[nestjs]]
# topics: #nestjs #nodejs #web-development
---
## Nest.js is a Node.js framework to build robust server-side applications.
Fully supports TypeScript yet still enables coding in pure JavaScript.

Under the hood, Nest makes use of robust HTTP Server frameworks like [Express](https://expressjs.com/) (the default) and optionally can be configured to use [Fastify](https://github.com/fastify/fastify) as well!

Nest provides a level of abstraction above these common Node.js frameworks (Express/Fastify), but also exposes their APIs directly to the developer. This gives developers the freedom to use the myriad of third-party modules which are available for the underlying platform.

## Basic commands to get started with a Nest.js project

```bash
$ npm i -g @nestjs/cli
$ nest new project-name
```

Then, you may proceed with a `cd project-name` and `npm run dev` to run the project locally. Navigate to `http://localhost:3000` to visualize your new project.

## Nest.js core idea is to support microservices.
Nest is one of the best frameworks to develop a web application with microservices. It's native support to things such as dependency injection, decorators, exception filters, pipes, guards and interceptors, apply equally to microservices. Wherever possible, Nest abstracts implementation details so that the same components can run across HTTP-based platforms, WebSockets, and Microservices.

In Nest, a microservice is fundamentally an application that uses a different **transport** layer than HTTP. And speaking of HTTP, **Nest uses HTTP server frameworks like Express (default) or Fastify (if user prefers)** to handle HTTP request and response cycles.

## New project overview
`main.ts` is the entry point of a Nest application, it is the main file of the application. It creates and builds the application importing a module, which is a class (named `AppModule`) which is also called **root module**. Speaking of modules, Nest uses decorators such as **@Module** to define what a class or a variable means and it's responsibilities, everything you build in Nest **has to be** inside a Module so it can be shared across the entire application.

Also, it has a MVC (Module-View-Controller) approach to separate responsibilities in many different layers and keep everything organized. 

Services are another fundamental concept of Nest. They are imported on your Controllers and may be used through HTTP requests that come from methods inside these Controllers.

## CLI
Nest has a fully native CLI from which you can create things for your application:

``` bash
nest g controller controllerName
```

This command creates a Controller on your application for example.


``` bash
nest g resource
``` 

This generates an entire new Module with its own Controller, Service and integrated tests. It also automatically updates the AppModule (root module) of the application so it imports and integrates the new Module correctly.

## Databases
Nest has native support to the best database tools of the Node.js ecossystem. Prisma, TypeORM, MikroORM, etc. are all natively supported and easy to use in a Nest application. 

Many of them e.g. TypeORM has an `npm` package that natively supports Nest and provides tools and syntax to integrate the ORM into your Nest application.
