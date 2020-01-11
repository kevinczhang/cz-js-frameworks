---
description: An AngularJS module defines an application.
---

# Modules

The module is a container for the different parts of an application. The module is a container for the application controllers. You can add controllers, directives, filters, and more, to your AngularJS module.

### Creating and register a Module

```javascript
// Create module1
var myModule = angular.module('module1', []);

// Register appservice in module1
angular.module('module1').service('appservice', function(appservice) {
   var serviceCall = $http.post('api/getUser()',"Role");
});

// Create myModule
var myModule = angular.module('myModule', ['module1','module2']);

// Use module1's appservice in myModule
angular.module('myModule').controller('appservice', function(appservice)
{
    var Servicedata= appservice.ServiceCall('role');
}
```

### Functions can Pollute the Global Namespace

Global functions should be avoided in JavaScript. They can easily be overwritten or destroyed by other scripts. AngularJS modules reduces this problem, by keeping all functions local to the module.



