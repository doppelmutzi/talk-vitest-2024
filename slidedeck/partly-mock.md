## Partially mock a module (I)

```ts [1-14|3-9]
import { describe, it, expect, vi } from 'vitest';
import * as myModule from './myModule';

vi.mock('./myModule', async () => {
  const originalModule = await vi.importActual
    <typeof myModule>('./myModule');
  return {
    ...originalModule,
    myFunction: vi.fn().mockReturnValue('mocked value'),
  };
});
it('Partially mock module with vi.mock', () => {
    // ...
});
```

---

## Partially mock a module (II)

```ts [1:]
it('Partially mock module with vi.mock', () => {
    const result1 = myModule.myFunction('test');
    const result2 = myModule.anotherFunction();

    expect(vi.isMockFunction(myModule.myFunction))
        .toBe(true);
    expect(vi.isMockFunction(myModule.anotherFunction))
        .toBe(false);

    expect(result1).toBe('mocked value');
    expect(result2).toBe('Another original value');
});
```