## Stub globals (I)

```ts
  test("stub window", () => {
    vi.stubGlobal("window", {
      innerWidth: 1024,
      innerHeight: 768,
    });

    expect(window.innerWidth).toBe(1024);
    expect(window.innerHeight).toBe(768);
  });
```

---

## Stub globals (II)

```ts
  test("stub console.log", () => {
    vi.stubGlobal("console", {
      log: vi.fn(),
    });

    console.log("Hello, World!");

    const log = vi.mocked(console.log);
    expect(log).toHaveBeenCalledWith("Hello, World!");
    expect(vi.isMockFunction(log)).toBe(true);
  });
```