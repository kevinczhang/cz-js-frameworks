---
description: >-
  Consider modules to be the same as JavaScript libraries. A set of functions
  you want to include in your application.
---

# Modules

## Built-in Modules

Node.js has a set of built-in modules which you can use without any further installation.

| Module                                                                       | Description                                                |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------- |
| [assert](https://www.w3schools.com/nodejs/ref\_assert.asp)                   | Provides a set of assertion tests                          |
| [buffer](https://www.w3schools.com/nodejs/ref\_buffer.asp)                   | To handle binary data                                      |
| child\_process                                                               | To run a child process                                     |
| [cluster](https://www.w3schools.com/nodejs/ref\_cluster.asp)                 | To split a single Node process into multiple processes     |
| [crypto](https://www.w3schools.com/nodejs/ref\_crypto.asp)                   | To handle OpenSSL cryptographic functions                  |
| [dgram](https://www.w3schools.com/nodejs/ref\_dgram.asp)                     | Provides implementation of UDP datagram sockets            |
| [dns](https://www.w3schools.com/nodejs/ref\_dns.asp)                         | To do DNS lookups and name resolution functions            |
| domain                                                                       | Deprecated. To handle unhandled errors                     |
| [events](https://www.w3schools.com/nodejs/ref\_events.asp)                   | To handle events                                           |
| [fs](https://www.w3schools.com/nodejs/ref\_fs.asp)                           | To handle the file system                                  |
| [http](https://www.w3schools.com/nodejs/ref\_http.asp)                       | To make Node.js act as an HTTP server                      |
| [https](https://www.w3schools.com/nodejs/ref\_https.asp)                     | To make Node.js act as an HTTPS server.                    |
| [net](https://www.w3schools.com/nodejs/ref\_net.asp)                         | To create servers and clients                              |
| [os](https://www.w3schools.com/nodejs/ref\_os.asp)                           | Provides information about the operation system            |
| [path](https://www.w3schools.com/nodejs/ref\_path.asp)                       | To handle file paths                                       |
| punycode                                                                     | Deprecated. A character encoding scheme                    |
| [querystring](https://www.w3schools.com/nodejs/ref\_querystring.asp)         | To handle URL query strings                                |
| [readline](https://www.w3schools.com/nodejs/ref\_readline.asp)               | To handle readable streams one line at the time            |
| [stream](https://www.w3schools.com/nodejs/ref\_stream.asp)                   | To handle streaming data                                   |
| [string\_decoder](https://www.w3schools.com/nodejs/ref\_string\_decoder.asp) | To decode buffer objects into strings                      |
| [timers](https://www.w3schools.com/nodejs/ref\_timers.asp)                   | To execute a function after a given number of milliseconds |
| [tls](https://www.w3schools.com/nodejs/ref\_tls.asp)                         | To implement TLS and SSL protocols                         |
| tty                                                                          | Provides classes used by a text terminal                   |
| [url](https://www.w3schools.com/nodejs/ref\_url.asp)                         | To parse URL strings                                       |
| [util](https://www.w3schools.com/nodejs/ref\_util.asp)                       | To access utility functions                                |
| v8                                                                           | To access information about V8 (the JavaScript engine)     |
| [vm](https://www.w3schools.com/nodejs/ref\_vm.asp)                           | To compile JavaScript code in a virtual machine            |
| [zlib](https://www.w3schools.com/nodejs/ref\_zlib.asp)                       | To compress or decompress files                            |

## Include Modules

To include a module, use the `require()` function with the name of the module:

```java
var http = require('http');

http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/html'});
  res.end('Hello World!');
}).listen(8080);
```

## Create Your Own Modules

Use the `exports` keyword to make properties and methods available outside the module file.

Example

Save the code above in a file called "myfirstmodule.js"

**var dt = require('./myfirstmodule');**
