
#### **Auto-Configuration
-  Configuration means, application must have some prerequisites to run, expose and externally needs some resources from outside, spring can configure via XML, spring boot used annotation or java classes. If it happens automatically without developer creates object its called auto-configuration.
- **Purpose of Auto-Configuration
	- Every developer must be setup their own application like web layer, data layer, instead of boilerplate code like micro-service they use Auto-configuration, now developer focus only their business logic.
- Spring allows to create [[#**Custom Auto-Configuration Steps|custom Auto-configuration class]]. But it runs before configuration annotation classes and scanning packages.
- Auto-configuration by default (Proxiesbean = false ) for fastly inject or creates beans. This is one the difference between @configuration annotation.
- 3.x spring uses META-INF/spring/\<autoconfiguration package>.imports file have all required classes path. Before 3.x spring used spring.factories file used to auto-configuration, which exists in auto-configuration jar file.
- It helps more on micro-service because different model needs to implement to avoid boilerplate code.
#### **Custom Auto-Configuration Steps
1. The class must annotated with @AutoConfiguration annotation. It similarly function like configuration class that difference is above fourth point mentioned.
2. Above topics last point is second steps (Modern Auto-configuration).
3. Above two steps enough for auto-configuration, but the last point of the topics explain how other application can uses, check Naming content to add dependencies in new project.
#### **IoC (Inversion of Control)
- Before understand IoC must learn [[#**Controls of Objects|Control of objects]].
- Inversion of controls meaning, it get dependencies dynamically get injects and use it.
- IoC is principles or design types to handles singleton application. Then how spring achieve that, using BeanFactory, this is handles all the beans and it's root interface, ApplicationContext also manage the bean implements BeanFactory as well as features like AOP.
-  Three types of handling,
		1. Creation
		2. Manage lifecycle (AutoWire, AOP).
		3. Instantiates (Initializing via constructor).
#### **Controls of Objects
-  The class or object which controls their dependencies directly or It's creates own dependencies object's and access.