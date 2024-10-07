## Structure tests

- **System Under Test (SUT)** represents the module that is being tested
- **Test Candidate** synonym for the SUT
- **Actors** entities that interact with the SUT during the test, such as other modules. 
<!-- If actors are complex modules, such as 3rd-party libraries, you might want to replace them with fake, simplified variants. These substitutes are called **test doubles**.  -->

---

## Organize tests

- **Arrange** set up the conditions for the test
- **Act** invoke the SUT.
- **Assert** verify that the SUT behaved as expected
- **Teardown** optional clean up, e.g., resetting test doubles.
