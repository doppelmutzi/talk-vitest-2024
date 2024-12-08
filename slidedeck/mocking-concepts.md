## Mocking concepts (I)

- **Test doubles** umbrella term for various types of objects used to replace real components
- **Dummies** placeholders to satisfy function signature, not involved in the actual logic being tested
- **Fakes** Lightweight working implementations making them unsuitable for prod (e.g., in-memory DB)

---

## Mocking concepts (II)

- **Stubs** functions providing predefined responses without recording usage information
- **Spies** stubs that also record information about their usage helping in the verification of expected behavior
- **Mocks** functions designed to anticipate and verify specific interactions, replacing the original implementation
