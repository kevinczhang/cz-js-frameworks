# Routing

&#x20;If you want to navigate to different pages in your application, but you also want the application to be a SPA (Single Page Application), with no page reloading, you can use the `ngRoute` module.

To make your applications ready for routing, you must include the AngularJS Route module:

```markup
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular-route.js"></script>
```

```markup
<body ng-app="myApp">

<p><a href="#/!">Main</a></p>

<a href="#!red">Red</a>
<a href="#!green">Green</a>
<a href="#!blue">Blue</a>

<div ng-view></div>

<script>
var app = angular.module("myApp", ["ngRoute"]);
app.config(function($routeProvider) {
  $routeProvider
  .when("/", {
    templateUrl : "main.htm"
  })
  .when("/red", {
    templateUrl : "red.htm"
  })
  .when("/green", {
    templateUrl : "green.htm"
  })
  .when("/blue", {
    templateUrl : "blue.htm"
  });
});
</script>
</body>
```

## &#x20;ng-view

There are three different ways to include the `ng-view` directive in your application:

```markup
<div ng-view></div>
<ng-view></ng-view>
<div class="ng-view"></div>
```

## Template

In the previous examples we have used the `templateUrl` property in the `$routeProvider.when` method.

You can also use the `template` property, which allows you to write HTML directly in the property value, and not refer to a page.

## otherwise method

In the previous examples we have used the `when` method of the `$routeProvider`.

You can also use the `otherwise` method, which is the default route when none of the others get a match.

