# Basics

### AngularJS Expressions

AngularJS binds data to HTML using Expressions. AngularJS expressions can be written inside double braces: `{{` _`expression`_ `}}`. AngularJS expressions can also be written inside a directive: `ng-bind="`_`expression`_`"`.

 **AngularJS expressions** are much like **JavaScript expressions:** They can contain literals, operators, and variables.

### AngularJS Expressions vs. JavaScript Expressions

1. Like JavaScript expressions, AngularJS expressions can contain literals, operators, and variables.
2. Unlike JavaScript expressions, AngularJS expressions can be written inside HTML.
3. AngularJS expressions do not support conditionals, loops, and exceptions, while JavaScript expressions do.
4. AngularJS expressions support filters, while JavaScript expressions do not.

## AngularJS Directives

 AngularJS lets you extend HTML with new attributes called **Directives**. AngularJS directives are extended HTML attributes with the prefix `ng-`.

#### ng-app

The `ng-app` directive initializes an AngularJS application.

#### ng-init

The `ng-init` directive initializes application data.

#### ng-repeat

The `ng-repeat` directive repeats an HTML element

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

#### ng-model

The `ng-model` directive binds the value of HTML controls \(input, select, textarea\) to application data. 

The `ng-model` directive can provide type validation for application data \(number, e-mail, required\)

```markup
<form ng-app="" name="myForm">
  Email:
  <input type="email" name="myAddress" ng-model="text">
  <span ng-show="myForm.myAddress.$error.email">Not a valid e-mail address</span>
</form>
```

 The `ng-model` directive can provide status for application data \(valid, dirty, touched, error\):

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

 The `ng-model` directive provides CSS classes for HTML elements, depending on their status:

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



