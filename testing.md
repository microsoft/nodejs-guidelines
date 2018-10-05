# Testing your Node.js app
An important part of writing any Node.js application is ensuring that your code is covered with rebust tests. This ensures that your application is functional, high quality, and as safe guarded from bugs as possible. 

# Types of Testing

## Unit Testing
Unit Testing is the process of testing the smallest testable part of your application and are intended to assert that each unit of the software performs as designed. 
Unit tests are usually used to validate that a function returns values correctly, and that it handles errors gracefully. This is accomplished by passing both correct and incorrect parameters to the function and assessing the output.

You can generally think of these tests as human readible assertions. For example, consider the following function:

```javascript
  function addOne(number) {
    return number + 1;
  }
```

The kinds of questions we could consider when writing our tests include:
- _Does `addOne` correctly return a number incremented by one?_
- _What happens when `addOne` doesn't receives a parameter?_
- _What happens when `addOne` receives a parameter that isn't a number?_

These questions not only direct you in how to test your function but also inform the design of the function itself, such as adding error handling for incorrect parameter types. 

The below example demonstrates how we can write a unit test, written using [Jest](#jest):
```javascript
test('1 + 1 to equal 2', () => {
  const result = addOne(1);
  expect(result).toBe(2);
});
```

If `addOne` is working as expected, the value of `result` should be `2` and the test should therefore pass.

## Intergration Testing
Integration Testing is the process of testing the interactions between multiple functions. They are intended to ensure that the combination of functions produces the correct results or behaviour.

Intergration tests are writen as test plans that outline a scenario, usually emulating the scripts or modules they are used in. Consider the below script:

```javascript
  function addOne(number) {
    return number + 1;
  }

  function sum(a, b) {
    return a + b;
  }

  const number = 1;
  const secondNumber = addOne(number);
  const total = sum(number, secondNumber)

  console.log(total) // returns 3
```

In this example, our tests assertions would be applied to the `total` varible, rather than the functions themselves. We would consider tests as scenarios, such as: 
- _If `number` is set to 1, would `total` correctly have a value of `3`?_
- _What happens when the value of `number` is a not a number?_


The below example demonstrates how we can write an intergration test, written using [Mocha](#mocha) and the [Node.js Assert Module]():

```javascript
const assert = require('assert');
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () => {
  const number = 1;
  const secondNumber = addOne(number);
  const total = sum(number, secondNumber)

  assert(total, 3);
});
```

## Node.js Assert Module
Node ships with a collection of built in modules out of the box, including it's own assertion module. It has a basic selection of comparison functions and can be coupled with a test runner like [Mocha](#mocha) to provide a lightweight testing solution.

Although possible, using the assert module is not recommended for writing tests for a Node application, due to the limited selection of assertions it offers. More robust assertion libraries like [Chai](#chai), or testing frameworks that supply their own assertion libraries like [Jest](#jest), can provide a more robust testing solution for your application.

For further details on the [Assert](https://nodejs.org/api/assert.html) module, check out the [Node.js documentation](https://nodejs.org/api/) for more information.


## Mocking HTTP/S Requests
Testing HTTP/S requests can be a challenging task, due to the asynchronous nature of sending and recieving data between your application and an external nature. 

I good solution for testing your requests is 
[Nock](https://github.com/nock/nock). 
The library is great for mocking and intercepting HTTP/S request and works by overriding Node's `http.request` function. It also overrides `http.ClientRequest` too to take modules that use the http module directly into account.


For further details on the [HTTP](https://nodejs.org/api/http.html) and [HTTPS](https://nodejs.org/api/https.html) modules, check out the [Node.js documentation](https://nodejs.org/api/) for more information.

## Testing Frameworks
Below is a selection of some of the most popular testing frameworks available, all of which can be used to test your Node application:

- [Jest](https://jestjs.io)
- [Mocha](https://mochajs.org/)
- [AVA](https://github.com/avajs/ava)
- [Jasmine](https://jasmine.github.io/)

## Testing Modules
Below are some useful modules that you can use when testing a Node.js application:

### Assertion
- [Chai](https://www.chaijs.com/)
- [Must.js](https://github.com/moll/js-must)

### Mocking, Stubbing, and Spying
- [mock-require](https://github.com/boblauer/mock-require)
- [Sinon](https://sinonjs.org/)
- [testdouble.js](https://github.com/testdouble/testdouble.js)
- [Nock](https://github.com/nock/nock)
- [AutoCannon](https://github.com/mcollina/autocannon)

### Reporting
- [Istanbul](https://istanbul.js.org/)

### Front End and Browser Testing
- [Karma](https://karma-runner.github.io/2.0/index.html)
- [Enzyme](https://airbnb.io/enzyme/)
- [Puppeteer](https://pptr.dev/)
- [Webdriver](http://webdriver.io/)
- [Cypress](https://www.cypress.io/)
- [Selenium](https://seleniumhq.github.io/selenium/docs/api/javascript/index.html)
