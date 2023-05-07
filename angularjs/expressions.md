# Basics

### AngularJS Expressions

AngularJS binds data to HTML using Expressions. AngularJS expressions can be written inside double braces: `{{`` `_`expression`_` ``}}`. AngularJS expressions can also be written inside a directive: `ng-bind="`_`expression`_`"`.

&#x20;**AngularJS expressions** are much like **JavaScript expressions:** They can contain literals, operators, and variables.

### AngularJS Expressions vs. JavaScript Expressions

1. Like JavaScript expressions, AngularJS expressions can contain literals, operators, and variables.
2. Unlike JavaScript expressions, AngularJS expressions can be written inside HTML.
3. AngularJS expressions do not support conditionals, loops, and exceptions, while JavaScript expressions do.
4. AngularJS expressions support filters, while JavaScript expressions do not.

## AngularJS Scope

The scope is the binding part between the HTML (view) and the JavaScript (controller).

All applications have a `$rootScope` which is the scope created on the HTML element that contains the `ng-app` directive. The rootScope is available in the entire application. If a variable has the same name in both the current scope and in the rootScope, the application uses the one in the current scope.

AngularJS provides filters to transform data:

* `currency` Format a number to a currency format.
* `date` Format a date to a specified format.
* `filter` Select a subset of items from an array.
* `json` Format an object to a JSON string.
* `limitTo` Limits an array/string, into a specified number of elements/characters.
* `lowercase` Format a string to lower case.
* `number` Format a number to a string.
* `orderBy` Orders an array by an expression.
* `uppercase` Format a string to upper case.

```markup
<div ng-app="myApp" ng-controller="personCtrl">

<p>The name is {{ lastName | uppercase }}</p>

</div>
```

## AngularJS Services

In AngularJS, a service is a function, or object, that is available for, and limited to, your AngularJS application. AngularJS has about 30 built-in services. One of them is the `$location` service.

### $http Service

```javascript
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $http) {
  $http.get("welcome.htm")
  .then(function(response) {
    $scope.content = response.data;
    $scope.statuscode = response.status;
    $scope.statustext = response.statusText;
  }, function(response) {
    // Second function handles error
    $scope.content = "Something went wrong";
  });
});
```

The response from the server is an object with these properties:

* `.config` the object used to generate the request.
* `.data` a string, or an object, carrying the response from the server.
* `.headers` a function to use to get header information.
* `.status` a number defining the HTTP status.
* `.statusText` a string defining the HTTP status.

### $timeout Service

```javascript
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $timeout) {
  $scope.myHeader = "Hello World!";
  $timeout(function () {
    $scope.myHeader = "How are you today?";
  }, 2000);
});
```

### $interval Service

```javascript
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $interval) {
  $scope.theTime = new Date().toLocaleTimeString();
  $interval(function () {
    $scope.theTime = new Date().toLocaleTimeString();
  }, 1000);
});
```

