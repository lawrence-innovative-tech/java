
#### **Spring data Jpa
- Before JPA, ORM frameworks like Hibernate had **their own APIs**.
- Each ORM had **different programming models**.
- The Java community created **JPA specification** to standardize ORM.
- Here, also using Reflection for mapping mapping objects.
- Spring data dependency is starter dependency, so it has autoconfiguration file
- When @Transactional exits in class it creates Spring AOP Proxy using beanPostProssesor in bean lifecycle.
- Jpa Repository extends Crud Repository and pagination Repository also. so, it can provide many implementations.
- Crud repository only provides Crud operations.

#### **@Transactional
- @Treansactional annotation manages ACID principle of Database.
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

#### **Hibernates
- ORM model has mapping rules
	- @OneToOne - It eager loading, two tables column directly involved.
	- @ManyToOne - it eager loading, Many entries connects one entry of another table.
	- @OneToMany - It Lazy loading, It runs first query when needs many query run one by one give result.
	- @ManyToMany - It Lazy loading, two types of large entries. using @JoinColumns to map entries.
- Initially executes one query then executes N query from executed query called N + 1 problems. Using JOIN FETCH avoids this  problems, but not always is efficient.

#### **Entity Lifecycle
- Transient - when entity creates.
- Persistent - When entity manages by entity manager in persistent context.
- Detached - After entity manager ends persistent context.
- Remove - Remove the row from the tables.

#### **Cascade
- Operation perform parent entities propagates to child entities.
- Types of Cascade
	- Persist - parent persist child also.
	- Merge - updating data from detach state in parent child also merge that.
	- Remove - if parent remove child also.
	- Refresh - if parent refresh child also.
	- Detach - If parent detach state child also detach state
	- ALL - all the above