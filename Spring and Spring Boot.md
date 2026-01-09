
#### **Auto-Configuration
-  Configuration means, application must have some requisites to run, expose and externally needs some resources from outside, spring should be configure via XML, spring boot used annotation or java classes. If it happens automatically without developer creates object its called auto-configuration.
- Every developer must be setup their own application like web layer, data layer, instead of boilerplate code like micro-service they use Auto-configuration, now developer focus only their business logic.
- It possible to create own Auto-configuration class also, to reduced
#### **IoC (Inversion of Control)
- Before understand IoC must learn [[#**Controls of Objects|Control of objects]].
- Inversion of controls meaning, it get dependencies dynamically get injects and use it.
- IoC is principles or design types to handles singleton application.
	- Three types of handling,
		1. Creation
		2. Manage lifecycle
		3. Instantiates
#### **Controls of Objects
-  The class or object which controls their dependencies directly or It's creates own dependencies object's and access.