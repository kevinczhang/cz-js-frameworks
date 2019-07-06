# Introduction to components

Angular creates, updates, and destroys components as the user moves through the application. Your app can take action at each moment in this lifecycle through optional lifecycle hooks, like ngOnInit\(\).

## Component metadata

The @Component decorator identifies the class immediately below it as a component class, and specifies its metadata.

The metadata for a component tells Angular where to get the major building blocks that it needs to create and present the component and its view.

## Data binding

![Logo Title Text 1](../../.gitbook/assets/databinding.png)

## Directives

When Angular renders them, it transforms the DOM according to the instructions given by directives. A directive is a class with a @Directive\(\) decorator.

A component is technically a directive. Angular defines the **@Component\(\)** decorator, which extends the **@Directive\(\)** decorator with template-oriented features.

In addition to components, there are two other kinds of directives: **structural** and **attribute**.

_Structural directives_ alter layout by adding, removing, and replacing elements in the DOM.

_Attribute directives_ alter the appearance or behavior of an existing element. In templates they look like regular HTML attributes, hence the name.

