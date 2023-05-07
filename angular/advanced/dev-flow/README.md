# Dev Flow

## Ahead-of-time (AOT) compilation

&#x20;The Angular ahead-of-time (AOT) compiler converts your Angular HTML and TypeScript code into efficient JavaScript code during the build phase _before_ the browser downloads and runs that code.&#x20;

Angular offers two ways to compile your application:

* _**Just-in-Time**_** (JIT)**, which compiles your app in the browser at runtime. This was the default until Angular 8.
* _**Ahead-of-Time**_** (AOT)**, which compiles your app and libraries at build time. This is the default since Angular 9.

### Advantages

1. &#x20;_Faster rendering_ With AOT, the browser downloads a pre-compiled version of the application.
2. &#x20;_Fewer asynchronous requests_ The compiler _inlines_ external HTML templates and CSS style sheets within the application JavaScript, eliminating separate ajax requests for those source files.
3. &#x20;_Smaller Angular framework download size_ There's no need to download the Angular compiler if the app is already compiled.&#x20;
4. &#x20;_Detect template errors earlier_ The AOT compiler detects and reports template binding errors during the build step before users can see them.
5. &#x20;_Better security_ AOT compiles HTML templates and components into JavaScript files long before they are served to the client.&#x20;

## Configuring application environments

```
└── src
    └── app
        ├── app.component.html
        └── app.component.ts
    └── environments
        ├── environment.prod.ts
        ├── environment.staging.ts
        └── environment.ts
```

&#x20;You can add additional configurations as required. To add a staging environment, create a copy of `src/environments/environment.ts` called `src/environments/environment.staging.ts`, then add a `staging` configuration to `angular.json`:

```
"configurations": {
  "production": { ... },
  "staging": {
    "fileReplacements": [
      {
        "replace": "src/environments/environment.ts",
        "with": "src/environments/environment.staging.ts"
      }
    ]
  }
}
```

To build using the staging configuration, run the following command:

```
ng build --configuration=staging
```

## Configuring size budgets

As applications grow in functionality, they also grow in size. The CLI allows you to set size thresholds in your configuration to ensure that parts of your application stay within size boundaries that you define.

&#x20;Define your size boundaries in the CLI configuration file, `angular.json`, in a `budgets` section for each configured environment.

When you configure a budget, the build system warns or reports an error when a given part of the app reaches or exceeds a boundary size that you set.

## Configuring CommonJS dependencies

&#x20;It is recommended that you avoid depending on CommonJS modules in your Angular applications. Depending on CommonJS modules can prevent bundlers and minifiers from optimizing your application, which results in larger bundle sizes. Instead, it is recommended that you use ECMAScript modules in your entire application.&#x20;

&#x20;The Angular CLI outputs warnings if it detects that your browser application depends on CommonJS modules. To disable these warnings, you can add the CommonJS module name to `allowedCommonJsDependencies` option in the `build` options located in `angular.json` file.

## Configuring browser compatibility

The CLI uses Autoprefixer to ensure compatibility with different browser and browser versions. You may find it necessary to target specific browsers or exclude certain browser versions from your build.

Internally, Autoprefixer relies on a library called Browserslist to figure out which browsers to support with prefixing. Browserlist looks for configuration options in a `browserslist` property of the package configuration file, or in a configuration file named `.browserslistrc`. Autoprefixer looks for the `browserslist` configuration when it prefixes your CSS.

* You can tell Autoprefixer what browsers to target by adding a browserslist property to the package configuration file, `package.json`:

```
content_copy"browserslist": [
  "> 1%",
  "last 2 versions"
]
```

* Alternatively, you can add a new file, `.browserslistrc`, to the project directory, that specifies browsers you want to support:

```
content_copy### Supported Browsers
> 1%
last 2 versions
```

## Proxying to a backend server

You can use the proxying support in the `webpack` dev server to divert certain URLs to a backend server, by passing a file to the `--proxy-config` build option. For example, to divert all calls for `http://localhost:4200/api` to a server running on `http://localhost:3000/api`, take the following steps.

1. Create a file `proxy.conf.json` in your project's `src/` folder.
2.  Add the following content to the new proxy file:

    ```
    content_copy{
      "/api": {
        "target": "http://localhost:3000",
        "secure": false
      }
    }
    ```
3.  In the CLI configuration file, `angular.json`, add the `proxyConfig` option to the `serve` target:

    ```
    content_copy...
    "architect": {
      "serve": {
        "builder": "@angular-devkit/build-angular:dev-server",
        "options": {
          "browserTarget": "your-application-name:build",
          "proxyConfig": "src/proxy.conf.json"
        },
    ...
    ```
4. To run the dev server with this proxy configuration, call `ng serve`.

#### Using corporate proxy <a href="#using-corporate-proxy" id="using-corporate-proxy"></a>

```
npm install --save-dev https-proxy-agent
```

When you define an environment variable `http_proxy` or `HTTP_PROXY`, an agent is automatically added to pass calls through your corporate proxy when running `npm start`.

Use the following content in the JavaScript configuration file.

```typescript
content_copyvar HttpsProxyAgent = require('https-proxy-agent');
var proxyConfig = [{
  context: '/api',
  target: 'http://your-remote-server.com:3000',
  secure: false
}];

function setupForCorporateProxy(proxyConfig) {
  var proxyServer = process.env.http_proxy || process.env.HTTP_PROXY;
  if (proxyServer) {
    var agent = new HttpsProxyAgent(proxyServer);
    console.log('Using corporate proxy server: ' + proxyServer);
    proxyConfig.forEach(function(entry) {
      entry.agent = agent;
    });
  }
  return proxyConfig;
}

module.exports = setupForCorporateProxy(proxyConfig);
```
