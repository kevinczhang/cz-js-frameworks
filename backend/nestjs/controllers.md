---
description: >-
  Controllers are responsible for handling incoming requests and returning
  responses to the client.
---

# Controllers

&#x20;`@Controller()` decorator, which is **required** to define a basic controller.

It's that simple. Nest provides the rest of the standard HTTP request endpoint decorators in the same fashion - `@Put()`, `@Delete()`, `@Patch()`, `@Options()`, `@Head()`, and `@All()`. Each represents its respective HTTP request method.

## **Request object**

```javascript
import { Controller, Get, Req } from '@nestjs/common';
import { Request } from 'express';

@Controller('cats')
export class CatsController {
  @Get()
  findAll(@Req() request: Request): string {
    return 'This action returns all cats';
  }
}
```

| `@Request()`              | `req`                               |
| ------------------------- | ----------------------------------- |
| `@Response(), @Res()`\*   | `res`                               |
| `@Next()`                 | `next`                              |
| `@Session()`              | `req.session`                       |
| `@Param(key?: string)`    | `req.params` / `req.params[key]`    |
| `@Body(key?: string)`     | `req.body` / `req.body[key]`        |
| `@Query(key?: string)`    | `req.query` / `req.query[key]`      |
| `@Headers(name?: string)` | `req.headers` / `req.headers[name]` |
| `@Ip()`                   | `req.ip`                            |

### **Status code**

```javascript
@Post()
@HttpCode(204)
create() {
  return 'This action adds a new cat';
}
```

### **Headers**

```javascript
@Post()
@Header('Cache-Control', 'none')
create() {
  return 'This action adds a new cat';
}
```

### **Redirection**

```javascript
@Get('docs')
@Redirect('https://docs.nestjs.com', 302)
getDocs(@Query('version') version) {
  if (version && version === '5') {
    return { url: 'https://docs.nestjs.com/v5/' };
  }
}
```

### **Route parameters**

```javascript
@Get(':id')
findOne(@Param('id') id): string {
  return `This action returns a #${id} cat`;
}

```

### **Request payloads**

```javascript
@Post()
async create(@Body() createCatDto: CreateCatDto) {
  return 'This action adds a new cat';
}

```

