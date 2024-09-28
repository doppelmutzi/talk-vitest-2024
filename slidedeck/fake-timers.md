## Testing timers

This is the second slide.

```ts
const fetchWithPolling = async (refetchInMillis: number) => {
  const poll = async () => {
    await fetch("https://dummyjson.com");

    setTimeout(poll, refetchInMillis);
  };

  poll();
};
```

---

## Fake timers

```ts
describe("fetchWithPolling", async () => {
  beforeAll(() => {
    vi.useFakeTimers();
  });

  afterAll(() => {
    vi.useRealTimers();
  });

  beforeEach(() => {
    vi.clearAllMocks();
  });
});
```

---

## Advance timers

```ts
 test("fetches at specified intervals", async () => {
    globalThis.fetch = vi.fn();
    const fetchMock = globalThis.fetch;
    await fetchWithPolling(1000);

    await new Promise(process.nextTick);
    expect(fetchMock).toHaveBeenCalledTimes(1);
    await vi.advanceTimersByTimeAsync(999);
    expect(fetchMock).toHaveBeenCalledTimes(1);
    await vi.advanceTimersByTimeAsync(2);
    expect(fetchMock).toHaveBeenCalledTimes(2);
    await vi.advanceTimersByTimeAsync(2000);
    expect(fetchMock).toHaveBeenCalledTimes(4);
  });
```