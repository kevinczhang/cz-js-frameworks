---
description: You can add AngularJS event listeners to your HTML elements
---

# Events

## Mouse Events

Mouse events occur when the cursor moves over an element, in this order:

1. ng-mouseover
2. ng-mouseenter
3. ng-mousemove
4. ng-mouseleave

Or when a mouse button is clicked on an element, in this order:

1. ng-mousedown
2. ng-mouseup
3. ng-click

```markup
<div ng-app="myApp" ng-controller="myCtrl">

<button ng-click="myFunction()">Click me!</button>

<p>{{ count }}</p>

</div>
<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
  $scope.count = 0;
  $scope.myFunction = function() {
    $scope.count++;
  }
});
</script>
```

## $event Object

You can pass the `$event` object as an argument when calling the function.
