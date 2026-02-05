there are three type of testing
1. unit - class, methods are validates here
2. integration - integrate multi modules here to validate
3. end to end - testing as user point 

Isolation
- Isolation is core principle because, the unit test focus on checks particular logic how does it will work.
- Never wait external dependencies like database connectivity, because it should identity how does the particular working, and easy to focus edge case also. because if it fail easy to identity where and why it failed.

how to achieve isolation
- Mock - mock depended object or dependency works like real one.
- Faking - Use memory database for real one.
- Stubbing - Setup before runs particular method or class all the necessary to stub.	 
- DI - direct inject to depends objects.

Testing structure(AAA patterns)
1. Arrange - before start test setup the env
2. Act - Test the actual 
3. Assert - checks expected result.

