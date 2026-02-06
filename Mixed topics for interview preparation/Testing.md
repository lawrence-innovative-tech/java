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

TDD - BDD
- TDD  is a Test Driven Development used to write test mechanism before writes actual code.
	1. RED is not yet creates actual code. under development or need to change the logic and to pass the test case.
	2. Green is the code written and test result as pass.
	3. Refactor is to add new think or make code to optimization.
BDD
- BDD is Behaviour Driven Development // Todo

Assertion and Matchers
- Assertion is used to match the result and expected output.
- Junit Assertion methods (basic)
	1. assertionEquals()
		1. assertEquals(actual, expected) all the primitive values
		2. assertEquals(actual, expected, String message) all the primitive values
		3. assertEquals(actual, expected, Supplier\<String>) all the primitive values
		4. Assertion.assertArraysEquals(actual[], expected[], String message) same as above mentions
		5. Assertion.assertIteratorEquals(actualIterator\<?>, ExpectedIterator\<?>, String message)
		
	2. assertion

Full Assertion list 
### Core equality & identity assertions

- assertEquals(expected, actual)
- assertEquals(expected, actual, String message)
- assertEquals(expected, actual, Supplier\<String> messageSupplier)
- Overloads for primitive types & special cases (with optional delta for floating-point):
    - assertEquals(boolean, boolean, ...)
    - assertEquals(byte, byte, ...)
    - assertEquals(char, char, ...)
    - assertEquals(short, short, ...)
    - assertEquals(int, int, ...)
    - assertEquals(long, long, ...)
    - assertEquals(float, float, float delta, ...)
    - assertEquals(double, double, double delta, ...)
- assertNotEquals(unexpected, actual, ...)
    - Same overloads exist for primitives, objects, float/double with delta
- assertSame(expected, actual, ...)
- assertNotSame(unexpected, actual, ...)

### Null & boolean checks

- assertNull(actual, ...)
- assertNotNull(actual, ...)
- assertTrue(boolean condition, ...)
- assertFalse(boolean condition, ...)

UnitTest lifecycle
- @BeforeAll - run once if present. by default it's static method if instance creates in class it will becomes instance methods. it runs only once.
- Creates object for @test if it method.
- @BeforeEach (junit4 @Before) - Before run each @Test, @RepeatedTest, @parametarizedTest method
- @Test - run test method.
- @AfterEach (junit4 @After) - run each @Test, it started to run if it test has failed.
- @AfterAll - run if present. it similar to @BeforeAll.
- The lifecycle for each test class. If wants to have single entry point singleton to use @TestContainers, @Containers, @Extendswith extension. 

**PER_METHOD** (default in JUnit 5)
    - New test class instance created **before each**@Test
    - Fields are **fresh/reset** for every test → very safe, isolated
    - @BeforeAll / @AfterAll **must be static**
    
**PER_CLASS** (opt-in via @TestInstance(Lifecycle.PER_CLASS))
    - One instance created for the **whole class**
    - Shared state between tests (careful!)
    - @BeforeAll / @AfterAll can be **non-static** (instance methods)
    - Great for expensive setup (e.g., Spring context, embedded DB) or when you want shared state intentionally


Handles exception
	@assertThrows(excepted_exception, () -> execution)
		Its helps to check negative scenario. if excepted exception won't throw the test failed.
Timeout habdling
	@Timeout(values = 2, unit = TimeUnit.SECONDS)
	assertTimeout(Duration.ofMillis(500), )