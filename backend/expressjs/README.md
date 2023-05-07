# ExpressJS

Express is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications.

```bash
npm install express --save
```

## Quick start

```javascript
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => res.send('Hello World!'))

app.listen(port, () => {
    console.log(`Example app listening at http://localhost:${port}`))
}
```

or use Express application generator

```javascript
npx express-generator
```

## Basic routing <a href="#basic-routing" id="basic-routing"></a>

Each route can have one or more handler functions, which are executed when the route is matched. Route definition takes the following structure:

```javascript
app.METHOD(PATH, HANDLER)
```

Where:

* `app` is an instance of `express`.
* `METHOD` is an [HTTP request method](https://en.wikipedia.org/wiki/Hypertext\_Transfer\_Protocol#Request\_methods), in lowercase.
* `PATH` is a path on the server.
* `HANDLER` is the function executed when the route is matched.

## Serving static files in Express <a href="#serving-static-files-in-express" id="serving-static-files-in-express"></a>

To serve static files such as images, CSS files, and JavaScript files, use the `express.static` built-in middleware function in Express.

The function signature is:

```
express.static(root, [options])
```

For example, use the following code to serve images, CSS files, and JavaScript files in a directory named `public`:

```javascript
app.use(express.static('public'))
```

Now, you can load the files that are in the `public` directory. To use multiple static assets directories, call the `express.static` middleware function multiple times:

```javascript
app.use(express.static('public'))
app.use(express.static('files'))
```

&#x20;To create a virtual path prefix (where the path does not actually exist in the file system) for files that are served by the `express.static` function, [specify a mount path](https://expressjs.com/en/4x/api.html#app.use) for the static directory, as shown below:

```javascript
app.use('/static', express.static(path.join(__dirname, 'public')))
```
