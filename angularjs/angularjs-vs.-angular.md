# AngularJS Vs. Angular

## **Architecture**

**AngularJS**

The architecture of AngularJS is based on model-view-controller \(MVC\) design. The model is the central component that expresses the application's behavior and manages its data, logic, and rules. The _view_ generates an output based on the information in the _model_. The _controller_ ****accepts input, converts it into commands and sends the commands to the _model_ and the _view_. 

**Angular** 

In Angular, controllers and $scope were replaced by components and directives. Components are directives with a template. They deal with a view of the application and logic on the page. There are two kinds of directives in Angular. These are structural directives that alter the layout of the DOM by removing and replacing its elements, and attributive directives that change the behavior or appearance of a DOM element. For web, mobile web, native mobile and native desktop.

## **Language**

**AngularJS**

AngularJS is written in JavaScript. 

**Angular**

Angular uses Microsoft’s TypeScript language, which is a superset of ECMAScript 6 \(ES6\). This has the combined advantages of the TypeScript features, like type declarations, and the benefits of ES6, like iterators and lambdas. ****TypeScript have powerful type checking and object-oriented features. 

##  **Databinding Syntax**

**AngularJS**

* **ng-model for two way binding.**
* ng-bind or {{ }} to bind model with html element in one way.
* The scope is the binding part between the HTML \(view\) and the JavaScript \(controller\).

  The scope is an object with the available properties and methods.

  The scope is available for both the view and the controller.

**Angular**

Angular focuses on “\( \)” for event binding and “\[ \]” for property binding.

##  **Module Support**

**AngularJS**

 All non-trivial Angular 1.x applications will bootstrap with a root module within an `ng-app` declaration in the main HTML file. A module is created by using the AngularJS function `angular.module`**.  Controllers and directives will be defined in the modules. Child modules will be injected into root module with DJ in constructor.**

**Angular**

 `ngModule` was introduce to make organizing and connecting components together much easier **with @NgModule annotation.**  The `@NgModule` decorator takes a configuration object that will typically contain imports, component declarations and if it is a top-level module, a reference to the component we want to bootstrap.  And instead of bootstrapping our top-level component directly, we will instead bootstrap our top-level module which is then responsible for delegating the implementation details. In this case, we know that when `AppModule` is instantiated, that it will in turn, instantiate the `AppComponent`.

## Performance

Angular is 5 times faster than AngularJS with the change detection mechanism from digest loop in AngularJS to a custom implementation by using zoneJs in Angular. Angular implements unidirectional tree-based change detection and uses Hierarchical Dependency Injection system. This significantly boosts performance for the framework.

## Mini App example

### AngularJS

{% code-tabs %}
{% code-tabs-item title="index.html" %}
```markup
<!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
<head/>
<body>

    <div ng-app="myApp" ng-controller="myCtrl">
        {{ firstName + " " + lastName }}
    </div>

<script src="myApp.js"></script>

</body>
</html>
```
{% endcode-tabs-item %}

{% code-tabs-item title="myApp.js" %}
```javascript
var app = angular.module("myApp", []);

app.controller("myCtrl", function($scope) {
  $scope.firstName = "John";
  $scope.lastName = "Doe";
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### **Angular**

**Angular CLI can help to initialize the app.**

{% code-tabs %}
{% code-tabs-item title="index.html" %}
```markup
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Architecture of Angular</title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <base href="/">

  <body>
    <app-root></app-root>
  </body>

</html>

```
{% endcode-tabs-item %}

{% code-tabs-item title="main.ts" %}
```typescript
import { enableProdMode } from '@angular/core';
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

import { AppModule } from './app/app.module';
import { environment } from './environments/environment';

if (environment.production) {
  enableProdMode();
}

platformBrowserDynamic().bootstrapModule(AppModule);

```
{% endcode-tabs-item %}

{% code-tabs-item title="app.module.ts" %}
```typescript
import { BrowserModule }       from '@angular/platform-browser';
import { FormsModule }         from '@angular/forms';
import { NgModule }     from '@angular/core';
import { AppComponent } from './app.component';
import { HeroDetailComponent } from './hero-detail.component';
import { HeroListComponent }   from './hero-list.component';
import { SalesTaxComponent }   from './sales-tax.component';
import { HeroService }         from './hero.service';
import { BackendService }      from './backend.service';
import { Logger }              from './logger.service';

@NgModule({
  imports: [
    BrowserModule,
    FormsModule
  ],
  declarations: [
    AppComponent,
    HeroDetailComponent,
    HeroListComponent,
    SalesTaxComponent
  ],
  providers: [
    BackendService,
    HeroService,
    Logger
  ],
  bootstrap: [ AppComponent ]
})
export class AppModule { }
```
{% endcode-tabs-item %}

{% code-tabs-item title="app.component.ts" %}
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <app-hero-list></app-hero-list>
    <app-sales-tax></app-sales-tax>
  `
})
export class AppComponent { }

```
{% endcode-tabs-item %}

{% code-tabs-item title="hero-list.component.ts" %}
```typescript
import { Component, OnInit }   from '@angular/core';

import { Hero }                from './hero';
import { HeroService }         from './hero.service';

@Component({
  selector:    'app-hero-list',
  templateUrl: './hero-list.component.html',
  providers:  [ HeroService ]
})
export class HeroListComponent implements OnInit {
  heroes: Hero[];
  selectedHero: Hero;

  constructor(private service: HeroService) { }

  ngOnInit() {
    this.heroes = this.service.getHeroes();
  }

  selectHero(hero: Hero) { this.selectedHero = hero; }
}

```
{% endcode-tabs-item %}

{% code-tabs-item title="hero.service.ts" %}
```typescript
import { Injectable } from '@angular/core';

import { Hero } from './hero';
import { BackendService } from './backend.service';
import { Logger } from './logger.service';

@Injectable()
export class HeroService {
  private heroes: Hero[] = [];

  constructor(
    private backend: BackendService,
    private logger: Logger) { }

  getHeroes() {
    this.backend.getAll(Hero).then( (heroes: Hero[]) => {
      this.logger.log(`Fetched ${heroes.length} heroes.`);
      this.heroes.push(...heroes); // fill cache
    });
    return this.heroes;
  }
}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

\*\*\*\*

