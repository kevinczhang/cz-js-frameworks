---
description: >-
  Nest (NestJS) is a framework for building efficient, scalable Node.js
  server-side applications.
---

# NestJS

&#x20;It uses progressive JavaScript, is built with and fully supports [TypeScript](http://www.typescriptlang.org/) (yet still enables developers to code in pure JavaScript) and combines elements of OOP (Object Oriented Programming), FP (Functional Programming), and FRP (Functional Reactive Programming).

&#x20;Under the hood, Nest makes use of robust HTTP Server frameworks like [**Express**](https://expressjs.com/) (the default) and optionally can be configured to use [**Fastify**](https://github.com/fastify/fastify) as well!

Nest provides a level of abstraction above these common Node.js frameworks (Express/Fastify), but also exposes their APIs directly to the developer. This allows developers the freedom to use the myriad of third-party modules which are available for the underlying platform.

## **Installation**

```
npm i -g @nestjs/cli
```

&#x20;Alternatively, to install the TypeScript starter project with **Git**:

```
$ git clone https://github.com/nestjs/typescript-starter.git project
$ cd project
$ npm install
$ npm run start
```

&#x20;You can also manually create a new project from scratch by installing the core and supporting files with **npm** (or **yarn**). In this case, of course, you'll be responsible for creating the project boilerplate files yourself.

```
$ npm i --save @nestjs/core @nestjs/common rxjs reflect-metadata
```

## core files:

| `app.controller.ts` | Basic controller sample with a single route.                                                                        |
| ------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `app.module.ts`     | The root module of the application.                                                                                 |
| `main.ts`           | The entry file of the application which uses the core function `NestFactory` to create a Nest application instance. |

The `main.ts` includes an async function, which will **bootstrap** our application:

{% code title="main.ts" %}
```javascript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```
{% endcode %}

