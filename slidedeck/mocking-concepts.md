## Mocking concepts (I)

- Test doubles: umbrella term for the following concepts 
- Dummies: values passed around and sometimes not even used (e.g., hard-coded customer object) <!-- .element: class="fragment" data-fragment-index="1" -->
- Fakes: Working implementations that take shortcuts making them unsuitable for prod (e.g., in-memory db) <!-- .element: class="fragment" data-fragment-index="2" --> 

---

## Mocking concepts (II)

- Stubs: functions that provide ready-made answers to the calls 
<!-- made during the test and generally do not respond to anything that has not been programmed for the test  -->
- Spies: Stubs that record information about how they are used, e.g., with which args called <!-- .element: class="fragment" data-fragment-index="1" --> 
<!-- helping in the verification of expected behavior -->
- Mocks: Pre-set functions designed to anticipate and specify the calls they should receive <!-- .element: class="fragment" data-fragment-index="2" --> 