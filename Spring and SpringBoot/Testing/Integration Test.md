
#### **Purpose
1. The unit test focus on only for main logic.
2. Integration test to check data flow, external dependency, configuration.
3. Junit create object outside of the application context, but spring creates application context for checks, When class annotated by @SpringBootTest, @DataJpaTest, @WebMvcTest or @TestContainers are used integration test and creates application context. Here, one problem is there that is mentioned in @InjectMock Definition.
4. Combine Mockito and Spring context in single class file, bean conflict will occur.
5. Mockito will executes first, so @InjectBean creates inject mock bean into controller, then spring started to executes it will scan and creates object in spring context, then spring starts di for PostProcessorBeanExecution to inject bean via reflection, now Controller class needs Service object, so spring initialize service class object from application context.

```java
@ExtendWith(MockitoExtension.class)  
@SpringBootTest(classes = KafkaProducerApplication.class)  
public class InjectMockTest {  
  
    @Mock  
    private Service service;  
  
    @InjectMocks  
    private Controller controller;  
  
    @BeforeEach  
    void setUp() {  
        System.out.println("controller: " + controller.hashCode());  
        System.out.println("service: " + service.hashCode());  
    }  
  
    @Test  
    public void injectMockTest() {  
        when(controller.getName()).thenReturn("test");  
        assertEquals(service.getName(), "test");  
    }  
}
```

#### **@SpringBootTest Annotation
- This annotation creates application context and maintain all the beans like spring runtime But it can also allows partial context like mocking, stubbing.
- Without application context, should mock all the bean or use raw java object creates and use.
- @SpringBootTest contains @WebMvcTest (for controller calling like api), @DataJpaTest (checks jpa transactions & functionality).
- If not annotate with, follow below method to manage beans
	1. Create raw java objects for every test.
	2. Create ApplicationContext object and configure.
	3. Use extension like @ExtensionWith(SpringExtension.class) + @ContextConfiguration(Configuration.class). For Junit4 use @RunsWith(SpringRunner.class).

#### **@MockBean, @SpyBean (Spring 6+, boot 3+ @MockitoBean, @MockitoSpyBean)

- It likes @Mock and @Spy but won't inject to application context, It for unit in isolation.
- **@MockBean, @SpyBean** Replaces real object instead of mock object in application context.
- **Workaround if stuck with @Mock/@Spy**:
	1. Use MockitoAnnotations.openMocks(this) in @BeforeEach to initialize them.
	2. Manually inject: ReflectionTestUtils.setField(service, "repo", repo); (hacky, brittle).
	3. But better: Switch to @MockBean/@SpyBean for seamless replacement.