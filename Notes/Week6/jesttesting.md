# Jest Unit Testing

Unit tests are code that calls our application's code and evaluates if our code is doing what it should be doing.

- In particular, it tests a small piece of code – usually a single function 

Tests do this via assertions, which is a fancy way of saying, "comparing expected vs. actual values". 

- Run the small piece of code with specific data and expect specific results.
- Do this for success cases and failure cases
  - i.e., we can "expect" failure when failure is the correct behavior



## Jest is a JavaScript testing framework



Jest is a popular JavaScript testing framework designed to ensure the correctness of applications. It provides a simple API, built-in assertion methods, and excellent support for asynchronous testing.



Unit testing is a software testing method where individual components of a program are tested in isolation. The goal is to validate that each unit of the software performs as expected. Jest simplifies this process with its intuitive syntax and built-in features.



## 🛠 Setting Up Jest

To start using Jest, follow these steps:

1. Install Jest as a development dependency:

```
npm install --save-dev jest
```

2. Ensure that the `package.json` file includes the following test script:

```
"scripts": {
  "test": "jest"
}
```

3. Run your tests with:

```
npm test
```



## 📌 Writing Your First Jest Test
A Jest test consists of a test suite (group of related tests) and individual test cases.

Example: Testing a Simple Function

Let's create a simple function that adds two numbers:
```js
// sum.js
function sum(a, b) {
  return a + b;
}
module.exports = sum;
```

Now, we write a Jest test for this function:

```
// sum.test.js
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});
```

### Running the Test

Run the test using:

```
npm test
```

If everything is correct, you should see output similar to this:

```js
PASS  ./sum.test.js
✓ adds 1 + 2 to equal 3 (5ms)
```



## 🛡 Jest Matchers

Jest provides built-in **matchers** to check values:

- **Basic Matchers**

  ```
  expect(2 + 2).toBe(4); // Strict equality
  expect({ foo: 'bar' }).toEqual({ foo: 'bar' }); // Deep equality
  ```

- **Truthiness**

  ```
  expect(null).toBeNull();
  expect(undefined).toBeUndefined();
  expect(0).toBeFalsy();
  ```

- **Numbers & Strings**

  ```
  expect(10).toBeGreaterThan(5);
  expect('Hello World').toMatch(/World/);
  ```

More matchers are available to cover various use cases.

## 🔄 Testing Asynchronous Code

Jest makes testing asynchronous code simple. You can test promises and async functions with:

### Example: Testing a Promise

```js
// asyncFunction.js
function fetchData() {
  return new Promise((resolve) => setTimeout(() => resolve('data'), 1000));
}
module.exports = fetchData;
```



```
// asyncFunction.test.js
const fetchData = require('./asyncFunction');

test('fetchData returns "data"', async () => {
  await expect(fetchData()).resolves.toBe('data');
});
```

## 🏗 Mocking Functions

Jest allows you to **mock** functions and modules to isolate unit tests:

```
const fetchData = jest.fn(() => 'mocked data');

console.log(fetchData()); // 'mocked data'
expect(fetchData).toHaveBeenCalled();
```

Mocking is useful when testing API calls, database operations, and external dependencies.



## 🎯 Organizing Tests

- Keep test files alongside the source files (e.g., `sum.test.js` next to `sum.js`)

- Use `describe()` blocks to group related tests

- Use `beforeEach()` and `afterEach()` to set up and clean up test environments

  

## 🔍 Unit Test vs Integration Test

### Unit Test

- Focuses on testing individual functions, methods, or classes in isolation.

- Ensures that a specific component works as expected.

- Uses mocks and stubs to replace dependencies.

- Typically fast and reliable.

- Example:

  ```
  test('adds 2 + 3 to equal 5', () => {
    expect(sum(2, 3)).toBe(5);
  });
  ```

### Integration Test

- Tests how multiple components work together.

- Ensures that interactions between modules function correctly.

- May involve databases, APIs, or external services.

- Slower than unit tests but provides higher confidence in system reliability.

- Example:

  ```
  test('fetches user data from API', async () => {
    const response = await fetch('/api/user');
    expect(response.status).toBe(200);
  });
  ```

  

## ✅ Conclusion

Jest is a powerful, easy-to-use testing framework that simplifies unit testing in JavaScript applications. By incorporating Jest into your development workflow, you can catch bugs early and ensure code reliability.

Explore [Jest's Documentation](https://jestjs.io/docs/getting-started) to dive deeper!



## 📚Resources

- [Jest Official Documentation](https://jestjs.io/docs/getting-started)
- [Jest GitHub Repository](https://github.com/jestjs/jest)
- https://jestjs.io/docs/expect
- https://jestjs.io/docs/asynchronous
- https://medium.com/bb-tutorials-and-thoughts/how-to-write-unit-tests-in-nodejs-with-jest-test-library-a201658829c7

