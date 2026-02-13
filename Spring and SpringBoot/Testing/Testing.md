there are three type of testing
1. unit - class, methods are validates here
2. integration - integrate multi modules here to validate
3. end to end - testing as user point 

Isolation
- Isolation is core principle because, the unit test focus on checks particular logic how does it will work.
- Never wait external dependencies like database connectivity, because it should identity how does the particular working, and easy to focus edge case also. because if it fail easy to identity where and why it failed.

how to achieve isolation
- Mock - mock depended object or dependency works like real one.
- Flaking - Use memory database for real one.
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

#### 1. **Overview of Bean Injection in Spring Tests**

- In Spring, beans are objects managed by the ApplicationContext (IoC container). Injection means providing dependencies automatically.
- In **tests**, injection helps set up realistic or mocked environments:
    - **Unit Tests**: Focus on isolating a single class (e.g., using Mockito to mock dependencies).
    - **Integration Tests**: Load part or all of the Spring context, injecting real or mocked beans.


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

Mock
- Mock is replace a real one. or mock is proxy object of implements interface or extends class.
- Simulate success, failure act as real object.
- Junit5 never pass class as parameter, it takes by reference.
Stub
- Stub is sub process of mock, mock is creates for proxy objects so, it should be returns if method has returns.
Spy
- Spy is a partial mock, it executes real code. if spy or particular method has stubbing, it defiantly returns stub's value. 
- When method has no stubbing, it will executes real one.

Inject Mock
- The construction injection is the best practice of managing or achieve IoC concept with DI concept.
- A Class wants some beans the inject Bean initializes those beans into particular class.
- It's like @Autowired in spring boot application.

#### **Type of Test methods (Junit5)
1. @ParameterizedTest
	1. @ValueSource - Processing a records like array.
	2. @CsvSource - Takes an entire row as parameter and process.
	3. @MethodSource - It should be in Arguments[], Stream\<Arguments>, Iterable\<Arguments>.
2. @RepeatedTest
3. @NestedTest
4. @DynamicTest

#### **Parameterized Test
- Parameterized test used to test application without calling external looping to runs the repeated or continue test methods.
- Pass input as parameter, there are three ways to pass parameter. that's all it mentions above.
	**@ValueSource**
	1. Process and pass every single value to start processing.
	2. It mostly test to primitive data types.
	3. Object can accept to create parameter test, but hardly to implement because of the parameter might not suitable to accept it.
	``` java
		@ParameterizedTest  
		@ValueSource(strings = {"ArrayList", "HashMap", "TreeMap", "TreeSet"})  
		public void checkParameterTest(String value) {  
		    System.out.println("Print parameter test :"+value);  
		}
	```
	   
	**@CsvSource**
	1. Process as differentiate as input using delimiter, but by default it's comma separator.
	2. Possible changing delimiter as user view.
	3. Input converts value as based on input types. But, can custom convert by using @ConvertWith.
	```java
	@ParameterizedTest  
	@CsvSource(value = {"test1|test2", "test3|test4"}, delimiter = '|')  
	public void checkCsvTest(String value1, String value2) {  
	    System.out.println("Print csv test :"+value1 + " - "+value2);  
	}
	```

	**@MethodSource
	1. Pass input from another method, but it should be in Argument of Stream, Iterable, arrays.
	2. Possible to create dynamic arguments to process.
	3. If method in different class must be mention as path of the class as parameter of annotation.
	4. Important think the method should be in static because it all the fields are generate for creating inputs. @TestInstance if per.class object only it's allowed to MethodSource in instance.
``` java
	@ParameterizedTest  
	@MethodSource(value = "checkMethodTest")  
	public void checkMethodTest(String value) {  
	    System.out.println("Print method test :"+value);  
	}  
  
	private static Stream<Arguments> checkMethodTest() {  
	    return Stream.of("test1", "test2", "test3").map(Arguments::of);  
	}
```

#### **Repeated Test
- Executes Sartain method or function particular count.
- While checking caching implementations speed time.
``` java
	@RepeatedTest(value = 5)  
	public void testAdd() {  
	    System.out.println("Test method - "+this.hashCode());  
	}
```

#### **Nested Test
- Easy test grouping test, like one success in method, but different scenario's multi testcase can perform as nested test instead of creating each test method.
- The nested test should be in inner class, it access outer class's objects.
- @DisplayName can easy to under not-technical as well as while through failed test case.
- By default it's not-static inner class.
- @NestedTest is equal to @Test so, the object creation functionalities are same as @Test. shown below examples.
``` java
  
@ExtendWith(MockitoExtension.class)  
public class ControllerTest {  
  
    @Mock  
    private Service service;  
  
    @InjectMocks  
    private Controller controller;  
  
    @Spy  
    private Service service1;  
   
    @BeforeEach  
    public void setUp() {  
//        service = mock();  
//        controller = new Controller(service);  
        System.out.println("controller :"+controller.hashCode());  
//        ReflectionTestUtils.setField(service, "host", service);  
    }  
  
    @ParameterizedTest  
    @ValueSource(strings = {"ArrayList", "HashMap", "TreeMap", "TreeSet"})  
    public void checkParameterTest(String value) {  
        System.out.println("Print parameter test :"+value);  
    }  
  
    @ParameterizedTest  
    @CsvSource(value = {"test1|test2", "test3|test4"}, delimiter = '|')  
    public void checkCsvTest(String value1, String value2) {  
        System.out.println("Print csv test :"+value1 + " - "+value2);  
    }  
  
    @ParameterizedTest  
    @MethodSource(value = "checkMethodTest")  
    public void checkMethodTest(String value) {  
        System.out.println("Print method test :"+value);  
    }  
  
    private static Stream<Arguments> checkMethodTest() {  
        return Stream.of("test1", "test2", "test3").map(Arguments::of);  
    }  
  
    @RepeatedTest(value = 5)  
    public void testAdd() {  
        System.out.println("Test method - "+this.hashCode());  
    }  
  
    @Nested  
    @DisplayName("checking display name")  
    public class NestedTestChecking {  
  
        @BeforeAll  
        static void setUpBeforeClass() throws Exception {  
            System.out.println("Setup before class");  
        }  
  
        @BeforeEach  
        public void setUp() throws Exception {  
            System.out.println("Setup before each");  
        }  
  
        @Test  
        public void testCheckBoolean() {  
            System.out.println("Test method - "+this.hashCode());  
        }  
    }  
}
```


#### **Dynamic Test
- Dynamic test check large to dataset without boilerplate, whereas creates each test as stream pipeline. 
- @BeforeEach won't invoke each dynamic test instead it will execute as first.
- @TestFactory annotation are used preparing test. Actually Junit triggers to method(), method perform completely triggers to factory, factory ends up, Junit starts execution.
- Test Factory has Dynamic node, dynamic node has Dynamic tests and Dynamic containers.
	examples :
``` java
@SpringBootTest
@AutoConfigureMockMvc
class UserApiDynamicTest {

    @Autowired
    MockMvc mockMvc;

    List<Integer> userIds = List.of(1,2,3);

    // -----------------------------
    // Dynamic tests for GET users
    // -----------------------------

    @TestFactory
    Stream<DynamicNode> userApiTests() {

        return Stream.of(

            // Container 1
            DynamicContainer.dynamicContainer("GET /users/{id}",
                userIds.stream()
                    .map(id ->
                        DynamicTest.dynamicTest(
                            "Fetch user " + id,
                            () -> mockMvc.perform(get("/users/" + id))
                                    .andExpect(status().isOk())
                                    .andExpect(jsonPath("$.id").value(id))
                        )
                    )
            ),

            // Container 2
            DynamicContainer.dynamicContainer("DELETE /users/{id}",
                userIds.stream()
                    .map(id ->
                        DynamicTest.dynamicTest(
                            "Delete user " + id,
                            () -> mockMvc.perform(delete("/users/" + id))
                                    .andExpect(status().isOk())
                        )
                    )
            )
        );
    }
}


```

Without Dynamic creates each @Test to validate all the methods.

