# Architecture

Angular is written in TypeScript. The basic building blocks of an Angular application are _NgModules_, which provide a compilation context for _components_.

An app always has at least a _root module_ that enables bootstrapping, and typically has many more _feature modules_.

* Components define _views_, which are sets of screen elements that Angular can choose among and modify according to your program logic and data.
* Components use _services_, which provide specific functionality not directly related to views. Service providers can be _injected_ into components as _dependencies_, making your code modular, reusable, and efficient.

Components define _views_ and use _services_, which provide specific functionality not directly related to views.

![Angular Architecture](../../.gitbook/assets/image-1%20%281%29.png)

