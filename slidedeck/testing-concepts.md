## Structuring tests

- **System Under Test (SUT)** represents the module that is being tested
- **Test Candidate** synonym for the SUT
- **Actors** entities that interact with the SUT during the test, such as other modules
<!-- If actors are complex modules, such as 3rd-party libraries, you might want to replace them with fake, simplified variants. These substitutes are called **test doubles**.  -->

---

## Organizing tests

- **Arrange** set up the conditions for the test
- **Act** invoke the SUT
- **Assert** verify that the SUT behaved as expected
- **Teardown** optional clean up, e.g., resetting test doubles

---

## Test candidate

```ts [1:]
// calculate.ts
import { logger } from "./logger";

export function calculate(num1, num2) {
  const result = num1 + num2;
  logger.log(`The result is ${result}`);
  return result;
}
```

---

## Test structure

```ts [1:]
// calculate.spec.ts
import { describe, expect, it, vi } from "vitest";
// Import the test candidate / SUT
import { calculate } from "./calculate";
// import the module to substitute (used inside of SUT)
import { logger } from "./logger";

// create test suite explicitly with describe
describe("calculate function", () => {
  // create actual test (alias for test)
  it("should log the result of the calculation", () => {
    // ...
  });
});
```

---

## Arrange

```ts [1: 3-8,11-13|1-2,9-10]
// mock the actor to prevent actual log output
vi.mock("./logger");
describe("calculate function", () => {
  it("should log the result of the calculation", () => {
    // Arrange: Set up the test candidate and the actors
    const num1 = 5;
    const num2 = 10;
    const expectedResult = 15;
    // gain access to the mock to assert on it later
    const loggerMock = vi.mocked(logger);
    // ...
  });
});
```

---

## Act and Assert

```ts [1: 1-6,13-14|7-12]
it("should log the result of the calculation", () => {
  // ...

  // Act: Call the SUT with the arranged args
  const result = calculate(num1, num2);

  // Assert: Check that the SUT behaved as expected
  // perform state verification
  expect(result).toBe(expectedResult);
  // perform behavior verification
  expect(loggerMock.log).toHaveBeenCalledWith(
    `The result is ${expectedResult}`
  );
});
```

---

## Cleanup / Teardown

```ts [1:]
describe("calculate function", () => {
  it("should log the result of the calculation", () => {
    // ...
  });

  afterEach(() => {
    // Clear all mocks to ensure a clean slate
    vi.clearAllMocks();
  });
});
```
