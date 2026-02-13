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