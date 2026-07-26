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

## Controllers

AngularJS controllers **control the data** of AngularJS applications. AngularJS controllers are regular **JavaScript Objects**.

```markup
<div ng-app="myApp" ng-controller="personCtrl">

First Name: <input type="text" ng-model="firstName"><br>
Last Name: <input type="text" ng-model="lastName"><br>
<br>
Full Name: {{fullName()}}

</div>

<script>
var app = angular.module('myApp', []);
app.controller('personCtrl', function($scope) {
  $scope.firstName = "John";
  $scope.lastName = "Doe";
  $scope.fullName = function() {
    return $scope.firstName + " " + $scope.lastName;
  };
});
</script>
```

## Custom Services

```javascript
app.service('hexafy', function() {
  this.myFunc = function (x) {
    return x.toString(16);
  }
});

app.controller('myCtrl', function($scope, hexafy) {
  $scope.hex = hexafy.myFunc(255);
});

app.filter('myFormat',['hexafy', function(hexafy) {
  return function(x) {
    return hexafy.myFunc(x);
  };
}]);
```

## Custom Directives

New directives are created by using the `.directive` function.&#x20;

To invoke the new directive, make an HTML element with the same tag name as the new directive. When naming a directive, you must use a camel case name, `w3TestDirective`, but when invoking it, you must use `-` separated name, `w3-test-directive.`

The legal restrict values are:

* `E` for Element name
* `A` for Attribute
* `C` for Class
* `M` for Comment

By default the value is `EA`, meaning that both Element names and attribute names can invoke the directive.

```markup
<body ng-app="myApp">

<w3-test-directive></w3-test-directive>

<script>
var app = angular.module("myApp", []);
app.directive("w3TestDirective", function() {
  return {
    template : "<h1>Made by a directive!</h1>"
  };
});
</script>

</body>
```

## Custom Filters

You can make your own filters by registering a new filter factory function with your module:

```markup
<ul ng-app="myApp" ng-controller="namesCtrl">
  <li ng-repeat="x in names">
    {{x | myFormat}}
  </li>
</ul>

<script>
var app = angular.module('myApp', []);
app.filter('myFormat', function() {
  return function(x) {
    var i, c, txt = "";
    for (i = 0; i < x.length; i++) {
      c = x[i];
      if (i % 2 == 0) {
        c = c.toUpperCase();
      }
      txt += c;
    }
    return txt;
  };
});
app.controller('namesCtrl', function($scope) {
  $scope.names = ['Jani', 'Carl', 'Margareth', 'Hege', 'Joe', 
  'Gustav', 'Birgit', 'Mary', 'Kai'];
});
</script>
```

