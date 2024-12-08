## Test doubles with Vitest API

- **vi.fn** creates standalone mock function, ideal for creating stubs used as arguments of the SUT
- **vi.spyOn** spies on an existing function with optional implementation override
- **vi.mock** mocks an entire module or specific functions, isolating the SUT from its dependencies

---

## Blurring Lines

- distinction between fakes, stubs, spies, and mocks is not as clear-cut
- all main APIs (**vi.fn**, **vi.spyOn**, **vi.mock**)
  - record usage information to verify interactions
  - can replace parts or the whole implementation
- **vi.fn** can act as a stub, spy, or mock

---

## Test candidate

```ts [1:]
// myModule.ts
export function myFunction(arg: string): string {
  return `Original value: ${arg}`;
}

export function anotherFunction(): string {
  return "Another original value";
}
```

---

## Mock entire module

```ts [1:]
import { describe, it, expect, vi } from 'vitest';
import * as myModule from "./myModule";
vi.mock("./myModule");
describe("Automatic mocking with vi.mock", () => {
  it("should mock all functions in the module", () => {
    expect(vi.isMockFunction(myModule.anotherFunction))
        .toBe(true);
    // Call a mocked function
    myModule.myFunction("test");
    // Verify the interaction
    expect(myModule.myFunction)
        .toHaveBeenCalledWith("test");
  });
});
```


---

## Spy on module

```ts [1:]
import { describe, it, expect, vi } from 'vitest';
import * as myModule from './myModule';
describe('Spy on myModule', () => {
  it('without changing its implementation', () => {
    const spy = vi.spyOn(myModule, 'anotherFunction');

    const result = myModule.anotherFunction();

    expect(vi.isMockFunction(myModule.anotherFunction))
        .toBe(true);
    expect(result).toBe('Another original value');
    expect(spy).toHaveBeenCalledTimes(1);
  });
});
```


---

## callback stub

```ts [1:]
import { describe, it, expect, vi } from 'vitest';
function processCallback(
    callback: (arg: string) => string, arg: string) {
        return callback(arg);
}

describe("Standalone mock (as stub)", () => {
  it("should return a predefined value", () => {
    const stub = vi.fn().mockReturnValue("mocked value");
    const result = processCallback(stub, "test");
    expect(result).toBe("mocked value");
    expect(stub).toHaveBeenCalledWith("test");
  });
});
```


