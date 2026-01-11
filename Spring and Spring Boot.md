
#### **Auto-Configuration
-  Configuration means, application must have some prerequisites to run, expose and externally needs some resources from outside all are configure automated developer focus only their business logic. Spring can configure via XML, spring boot used annotation or java classes.
- **Purpose of Auto-Configuration
	- Every developer must be setup their own application like web layer, data layer, instead of boilerplate code like micro-service they use Auto-configuration, now developer focus only their business logic.
- Spring allows to create [[#**Custom Auto-Configuration Steps|custom Auto-configuration class]]. But it runs before configuration annotated classes and scanning packages.
- Auto-configuration by default (proxiesbean = false) for fastly inject or creates beans. This is one the difference between @Configuration annotation to @AutoConfiguration annotation.
- 3.x spring uses META-INF/spring/\<autoconfiguration package>.imports file have all required class path. Before 3.x spring used spring.factories file used to auto-configuration, which exists in auto-configuration jar file.
- It helps more on micro-service because different model needs to implement to avoid boilerplate code.
#### **Custom Auto-Configuration Steps
1. The class must annotated with @AutoConfiguration annotation. It similarly function like configuration class that difference is above fourth point mentioned.
2. Above topics fifth point is second steps (Modern Auto-configuration).
3. Above two steps enough for auto-configuration, but the last point of the topics explain how other application can uses, check Naming content to add dependencies in new project.
#### **IoC (Inversion of Control)
- Before understand IoC must learn [[#**Controls of Objects|Control of objects]].
- Inversion of controls meaning, it inject beans or dependencies dynamically and use it.
- IoC is principles or design types to handles singleton application. Then how spring achieve that, using BeanFactory, this is handles all the beans and it's root interface, ApplicationContext also manage the bean implements BeanFactory as well as features like AOP.
-  Three types of handling,
		1. Creation
		2. Manage lifecycle (AutoWire, AOP).
		3. Instantiates (Initializing via constructor).
#### **Controls of Objects
-  The class or object which controls their dependencies directly or It's creates own dependencies object's and access.

#### **Dependency Injection
- It's technique to achieve IoC principles to object handles in spring. There are three type of DI.
	1. Constructor Injection (Recommended)
	2. Setter Injection
	3. Field Injection
- Key features of Constructor Injector and why it's recommended
	- **Immutability -** Via constructor injection can protect bean using final keyword, the final should allows direct initialization and constructor to assign values. But, field injection couldn't achieve. Because, if initialize at creates via new keyword it creates object of every usage so, can't achieve singleton design patterns.
	- **Type safety (fail safety & fail fast) - ** Constructor injection forced to required all necessary bean, If it missed the application fail fast. But, field injection initial call empty constructor. So, no garaentee  
	- **Constructor Injection -** It's achieves IoC principles. 
	- **Unit testing -** Easy to integrate unit testing, If using field injection should use @MockBean annotation. 
	   