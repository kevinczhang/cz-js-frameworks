# Built-in Directives

AngularJS lets you extend HTML with new attributes called **Directives**. AngularJS directives are extended HTML attributes with the prefix `ng-`.

## ng-app: initializes an AngularJS application.

## ng-init: initializes application data.

## ng-repeat: repeats an HTML element

```markup
<div ng-app="" ng-init="quantity=1;price=5;names=['Jani','Hege','Kai']">

Quantity: <input type="number" ng-model="quantity">
Costs:    <input type="number" ng-model="price">

Total in dollar: {{ quantity * price }}
  
</div>
<ul>
   <li ng-repeat="x in names">
     {{ x }}
   </li>
</ul>

</div>
```

## ng-model: binds the value of HTML controls to application data.&#x20;

The `ng-model` directive can provide type validation for application data (number, e-mail, required)

```markup
<form ng-app="" name="myForm">
  Email:
  <input type="email" name="myAddress" ng-model="text">
  <span ng-show="myForm.myAddress.$error.email">Not a valid e-mail address</span>
</form>
```

&#x20;The `ng-model` directive can provide status for application data (valid, dirty, touched, error):

```markup
<form ng-app="" name="myForm" ng-init="myText = 'post@myweb.com'">
  Email:
  <input type="email" name="myAddress" ng-model="myText" required>
  <h1>Status</h1>
  {{myForm.myAddress.$valid}}
  {{myForm.myAddress.$dirty}}
  {{myForm.myAddress.$touched}}
</form>
```

&#x20;The `ng-model` directive provides CSS classes for HTML elements, depending on their status:

```markup
<style>
input.ng-invalid {
  background-color: lightblue;
}
</style>
<body>

<form ng-app="" name="myForm">
  Enter your name:
  <input name="myName" ng-model="myText" required>
</form>
```

## ng-options

&#x20;If you want to create a dropdown list, based on an object or an array in AngularJS, you should use the `ng-options` directive:

```markup
<div ng-app="myApp" ng-controller="myCtrl">
  <select ng-model="selectedName" ng-options="x for x in names">
  </select>
</div>

<select ng-model="selectedCar" ng-options="x for (x, y) in cars">
</select>

<h1>You selected: {{selectedCar}}</h1>

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
  $scope.names = ["Emil", "Tobias", "Linus"];
  $scope.cars = {
    car01 : {brand : "Ford", model : "Mustang", color : "red"},
    car02 : {brand : "Fiat", model : "500", color : "white"},
    car03 : {brand : "Volvo", model : "XC90", color : "black"}
  };
});
</script>
```

## **ng-disabled**&#x20;

This directive binds AngularJS application data to the disabled attribute of HTML elements.

```markup
<button ng-disabled="mySwitch">Click Me!</button>
```

## **ng-show**&#x20;

This directive shows or hides an HTML element.

```markup
<p ng-show="true">I am visible.</p>

<p ng-show="false">I am not visible.</p>
```

## **ng-hide**&#x20;

This directive hides or shows an HTML element.

```markup
<p ng-hide="true">I am not visible.</p>

<p ng-hide="false">I am visible.</p>
```
