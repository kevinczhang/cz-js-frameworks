---
description: 'NPM is a package manager for Node.js packages, or modules if you like.'
---

# NPM

A package in Node.js contains all the files you need for a module.

Modules are JavaScript libraries you can include in your project.

```bash
C:\Users\Your Name>npm install upper-case
```

```javascript
var http = require('http');
var uc = require('upper-case');
http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/html'});
  res.write(uc("Hello World!"));
  res.end();
}).listen(8080);
```

