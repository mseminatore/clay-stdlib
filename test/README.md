# stdlib/test

A simple, colorful testing framework for the [Clay](https://github.com/mseminatore/clay) programming language.

## Installation

Part of the Clay standard library, which ships with Clay — no install needed.

## Quick Start

```clay
import("stdlib/test")

Test describe("Math") {
    Test it("adds numbers") {
        Test assertEqual(1 + 1, 2)
    }

    Test it("subtracts numbers") {
        Test assertEqual(10 - 4, 6)
    }
}

Test run
```

Output:

```
  Math
    ✓ adds numbers
    ✓ subtracts numbers

2 tests, 2 passed, 0 failed
```

## API

### `Test describe(name, block)`

Groups related tests under a named suite. Suites can be nested; a failure is
reported with the full path (`String > concat > joins`). An error raised in a
suite outside any `it` counts as a failed test.

```clay
Test describe("String") {
    Test it("concatenates") {
        Test assertEqual("a" + "b", "ab")
    }
}
```

### `Test it(name, block)`

Defines a single test case. Exceptions are caught and reported as failures.

```clay
Test it("divides") {
    Test assertEqual(10 / 2, 5)
}
```

### `Test assertEqual(actual, expected)`

Asserts that two values are equal. Raises an error with a descriptive message on failure
(`expected "1" but got 1`: strings are quoted, so a type mismatch is visible).

### `Test assertNotEqual(actual, expected)`

Asserts that two values are not equal.

### `Test assertTrue(value)`

Asserts that the value is exactly `true` (`nil`, `1` or `"yes"` fail).

### `Test assertFalse(value)`

Asserts that the value is exactly `false` (`nil` fails).

### `Test assertRaises(block, errorType)`

Asserts that the block raises an error and returns it. With `errorType`, the error
must be of that type.

```clay
Test it("catches division by zero") {
    Test assertRaises({ 1 / 0 }, "DivisionByZero")
}

Test it("reports what is wrong") {
    e = Test assertRaises({ raise("bad input") })
    Test assertEqual(e message, "bad input")
}
```

### `Test run`

Prints the test summary. Call this after all `describe` blocks. If any test
failed, it lists the failures and exits with status 1, so CI and `ctest` see
the failure.

```clay
Test run
// => 5 tests, 5 passed, 0 failed
```

## Output

Colors are used only when output goes to a terminal and the `NO_COLOR`
environment variable is not set.

- Suite names are displayed in **bold cyan**
- Passing tests show a green **✓** with dimmed test name
- Failing tests show a red **✗** with the test name
- The summary line is green when all tests pass, red when any fail
- Failed tests are listed with their suite, name, and error message

## License

MIT
