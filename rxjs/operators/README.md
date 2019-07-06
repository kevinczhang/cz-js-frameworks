---
description: Operators are functions.
---

# Operators

### There are two kinds of operators:

* Pipeable Operators are the kind that can be piped to Observables using the syntax observableInstance.pipe\(operator\(\)\). A Pipeable Operator is a function that takes an Observable as its input and returns another Observable. It is a pure operation: the previous Observable stays unmodified.
* Creation Operators are the other kind of operator, which can be called as standalone functions to create a new Observable.

## **Piping**

Pipeable operators are functions, so they _could_ be used like ordinary functions: `op()(obs)` — but in practice, there tend to be many of them convolved together, and quickly become unreadable: `op4()(op3()(op2()(op1()(obs))))`. For that reason, Observables have a method called `.pipe()` that accomplishes the same thing while being much easier to read:

```typescript
obs.pipe(
	op1(),
	op2(),
	op3(),
	op3(),
)
```

## **Higher-order Observables**

Observables most commonly emit ordinary values like strings and numbers, but surprisingly often, it is necessary to handle Observables _of_ Observables, so-called higher-order Observables.

## Categories of operators

There are operators for different purposes, and they may be categorized as: creation, transformation, filtering, joining, multicasting, error handling, utility, etc.

* Creation Operators
* Join Creation Operators
* Transformation Operators
* Filtering Operators
* Join Operators
* Multicasting Operators
* Error Handling Operators
* Utility Operators
* Conditional and Boolean Operators
* Mathematical and Aggregate Operators

