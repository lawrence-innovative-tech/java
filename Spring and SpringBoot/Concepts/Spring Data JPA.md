
#### **Spring data Jpa
- Before JPA, ORM frameworks like Hibernate had **their own APIs**.
- Each ORM had **different programming models**.
- The Java community created **JPA specification** to standardize ORM.
- Here, also using Reflection for mapping mapping objects with help of Jackson.
- Spring data dependency is starter dependency, so it has autoconfiguration file
- When @Transactional exits in class it creates Spring AOP Proxy using beanPostProssesor in bean lifecycle.
- Jpa Repository extends Crud Repository and pagination Repository also. so, it can provide many implementations.
- Crud repository only provides Crud operations.

#### **@Transactional
- @Treansactional annotation give ACID principle of Database.
- When @Transactional annotated method or class invokes Proxy calls it call EntityManagerFactory to get Entity Manager and binds to current thread using Thread-local mechanism. Each transaction is unique till the end. But it allows Propagation (means @Transactional have another @Transactional transaction bind or separate).
	- Propagations
		1. REQUIRED - By default, required it bind both transaction together.
		2. REQUIRED_NEW - Always creates new transaction and maintained.
		3. SUPPORT - Won't create transactional for sub transaction.
		4. NOT_SUPPORT - Won't create transaction.
		5. MANDATORY - 
		6. NESTED - 
- Problems of @Transactional annotations
  1. If method invoke inside @Transactional method, it won't work because proxy never called it executes normal.
  2. After Entity manager creates thread binds, begin the statement then executes our code or method it stores first level cache and modification happens methods end entity manager commit and if it throw Runtime exception it rollback. if user handles catches the error spring it it not a exception so, it commit the transaction.

#### **ACID**
Atomicity - complete or nothing.
Consistency - checks constraints if not rollback.
Isolation - Each transaction runs unique, don't see intermediate state.
Durability - Once commit the transaction after system crush, still data recover. Because before storing the data Write-ahead log(wal) first. then, stores the data. log in local disk immediately.

