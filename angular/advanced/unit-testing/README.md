# Unit testing

When we talking about testing in Angular we are usually talking about two different types of testing:

#### Unit Testing

This is sometimes also called _Isolated_ testing. It’s the practice of testing small isolated pieces of code. If your test uses some external resource, like the network or a database, it’s _not_ a unit test.

#### Functional Testing

This is defined as the testing of the complete functionality of an application. In practice with web apps, this means interacting with your application as it’s running in a browser just like a user would interact with it in real life, i.e. via clicks on a page.

This is also called _**End To End**_ or _**E2E**_ testing.

## Tools and frameworks

### Jasmine

Jasmine is a behavior-driven development framework for testing JavaScript code. Jasmine, and BDD in general, attempts to describe tests in a human readable format so that non-technical people can understand what is being tested.

* `describe(string, function)` function defines what we call a _Test Suite_, a collection of individual _Test Specs_.
* &#x20;`it(string, function)` function defines an individual _Test Spec_, this contains one or more _Test Expectations_.
* &#x20;`expect(actual)` expression is what we call an _Expectation_. In conjunction with a _Matcher_ it describes an _expected_ piece of behaviour in the application.  `matcher(expected)` expression is what we call a _Matcher_. It does a boolean comparison with&#x20;
* &#x20;`expected` value passed in vs. the `actual` value passed to the `expect` function, if they are false the _spec_ fails.

### Built-in matchers

```typescript
expect(array).toContain(member);
expect(fn).toThrow(string);
expect(fn).toThrowError(string);
expect(instance).toBe(instance);
expect(mixed).toBeDefined();
expect(mixed).toBeFalsy();
expect(mixed).toBeNull();
expect(mixed).toBeTruthy();
expect(mixed).toBeUndefined();
expect(mixed).toEqual(mixed);
expect(mixed).toMatch(pattern);
expect(number).toBeCloseTo(number, decimalPlaces);
expect(number).toBeGreaterThan(number);
expect(number).toBeLessThan(number);
expect(number).toBeNaN();
expect(spy).toHaveBeenCalled();
expect(spy).toHaveBeenCalledTimes(number);
expect(spy).toHaveBeenCalledWith(...arguments);
```

### Setup and teardown

Sometimes in order to test a feature we need to perform some setup, perhaps it’s creating some test objects. Also we may need to perform some cleanup activities after we have finished testing, perhaps we need to delete some files from the hard drive.

These activities are called _setup_ and _teardown_ (for cleaning up) and Jasmine has a few functions we can use to make this easier:

1. beforeAll: This function is called **once**, _before_ all the specs in `describe` test suite are run.
2. afterAll: This function is called **once** _after_ all the specs in a test suite are finished.
3. beforeEach: This function is called _before_ **each** test specification, `it` function, has been run.
4. afterEach: This function is called _after_ **each** test specification has been run.

## Karma

Karma is a tool which lets us spawn browsers and run jasmine tests inside of them all from the command line.&#x20;

It’s not necessary to know the internals of how Karma works. When using the Angular CLI it handles the configuration for us and for the rest of this section we are going to run the tests using only Jasmine.

## Disabled and focused tests

You can disable tests without commenting them out by just pre-pending `x` to the `describe` or `it`functions.

&#x20;Conversely you can also focus on specific tests by pre-pending with `f.`
