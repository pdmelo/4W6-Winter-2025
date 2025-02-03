# Testing

The test files are typically kept in a directory named `./tests/` within the project’s root directory. Each test file contains one or more test suites, which are defined using the `describe` function. Within each test suite, there are individual tests, defined using the `it` or `test` function. These tests specify the expected behavior of the code being tested.

To run the tests, you can use the command `npm test` in the terminal. This command will execute all the test files in the project.

> [!TIP]
>
> I highly recommend running **one test at a time** while working.

To run an individual test, you can use the `--testNamePattern` option with `npm test`. For example, to run a test with the name “Todo was created.”, you can use the following command:

Terminal window

```
npm test -- --testNamePattern="Todo was created."
```

Alternatively, you can stick the `.only` function on the test in the suite like this:

```
http.test.ts;

test.only("Todo was created.", async () => {});
```

To run just one test suite, you can write the name of the file, or just the start of the file name:

Terminal window

```
npm test model

# or

npm test model.test.ts
```