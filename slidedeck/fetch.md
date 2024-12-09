## Mock fetch (I)

```ts [1:]
test("variant with globalThis.fetch", async () => {
    const dummyData = { message: "hey" };
    const stubResponse = {
      ok: true, statusText: "OK",
      json: async () => dummyData,
    } as Response;

    globalThis.fetch = vi.fn()
        .mockResolvedValue(stubResponse);
    const response = 
        await fetch("https://dummyjson.com/products");
    const data = await response.json();
    expect(data).toEqual(dummyData);
});
```

---

## Mock fetch (II)

```ts [1:]
test("variant with vi.stubGlobal", async () => {
    const dummyData = { data: "hey" };
    const dummyBlob = new Blob();
    vi.stubGlobal("fetch",
        vi.fn(() => Promise.resolve({
            blob: async () => dummyBlob,
            json: () => dummyData,
        })));
    const response = await fetch("dummyUrl");
    const data = await response.json();
    const blob = await response.blob();
    expect(data).toEqual(dummyData);
    expect(blob).toEqual(dummyBlob);
});
```