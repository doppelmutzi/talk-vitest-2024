## Parameterized tests

```ts [1:]
import { test, expect } from "vitest";

const inputs = ["Hello", "world", "!"];

test.each(inputs)("Testing string lengths of %s", 
    (input) => {
  expect(input.length).toBeGreaterThan(0);
});
```