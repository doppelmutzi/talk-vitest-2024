## Expecting errors (I)

```ts [1:]
it("should throw error", () => {
    expect(() => {
        throw new Error("Error message");
    }).toThrow("Error message");
});
```

---

## Expecting errors (II)

```ts [1:]
it("should throw error aft. rejected fetch", async () => {
    const errMsg = "Network error";
    vi.stubGlobal(
        "fetch",
        vi.fn(() => Promise.reject(new Error(errMsg))),
    );

    await expect(fetch("https://api.example.com")).
        rejects.toThrow(errMsg);
});
```