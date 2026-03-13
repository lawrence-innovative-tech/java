
#### **Spring data Jpa
- Java persistence api - group comity decide each provides use different type of implementation herd to implement and maintenance. so, comity decide and creates JPA. Every providers use JPA specification. It's uses ORM (Object Relation Mapping) mythologies.
- Here, also using Reflection for mapping mapping objects with help of Jackson.
- Spring data dependency is starter dependency, so it has autoconfiguration file
- When @Transactional exits in class it creates Spring AOP Proxy using beanPostProssesor in bean lifecycle.

#### **@Transactional
- @Treansactional annotation give ACID principle of Database.
- When @Transactional annotated method or class invocation