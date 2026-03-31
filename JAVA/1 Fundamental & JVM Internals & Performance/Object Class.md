 #### **Purpose
 - Object class is parent class of all the classes which user creates or build-in. So, it help to generics.
 - Object class provides necessary thinks of the each class. like getClass() to access current object.
 - Reflection, serialization and Threads are access via object class.
 - Object header layout 8-byte (64- Hotspot vm, compressedOops + compressedClassPointer).
 - [[#**getClass() - (Class object)|getClass()]] method is native final method can't overridden, getClass() calls native method get klass pointer, and communicate to Class object which is present in heap memory.
 - By default hava must extends only one class at a time, so if custom or build-in class extends some other classes jvm automatically writes object extension of parent class.
 - Delegation of lifecycle - B -> A -> object class.

#### **Object class methods
1. hashcode - by default it generate hash of memory it can overrides it will generate based on that.
2. equlas - by default it will checks references, when the class overrides checks based on overriden.
3. toString - by default it will print classname + hashcode of object, based on overriden it will print.
4. notify -
5. notifyall -
6. wait -
7. clone - 
8. finalize - when object will destroy gc calls finalize method but now it deprecated, this clear the used value of that object.

Your understanding was correct on every major point:

- HashCode first → mixing (xor inside fingerprint) → mask with (n-1) → bucket.
- Inside bucket: quick hash match → then equals check (custom or default).
- When equals is true → override the value (“override the content”).
- When equals is false → just add as another resident in the same bucket.
#### **Purpose of HashCode & equals
- Actually, Hash based collection buckets allocation will occur Collision, because if two object have same content but both are different hashcode hashmap allocates different buckets.
- But it may same person creates two times of object with same content java treats as different person, different content is collision, logically failed.
- If it override content and checks whether both have same content or not. if it both meets same it should allocates same buckets or it should be overrides.
- But, by default hashmap checks initially hashcode, if already buckets have values checks whether where both content are same using equals method. if same overrides or add new or consider new records. so when equals and hashcode both usage is powerful.
#### **HashCode
- If class doesn't override hashcode, the object creates (object memory address + timestamp) as default hashcode. the hashcode store it in mark word.
- By default, object creates it's generate unique hash for memory (Mark down) + memory address. but if it will overrides will creates new hash.
- While object creation there is no hashcode present in mark word. It is fully optional but, when obj.hashCode() invoked mark word stores that hashcode into object header incense mark word.
#### **IdentityHashCode
- Initially, IdentityHashCode and HashCode both are hold same value (object address + timestamp). But, when hashcode overrides by obj.hashCode() HashCode will updated, Still identityhashcode never changed, it's consent.
- The technique to prevent deadlock scenario. Because, every object must have identityhashcode comparison of two object locking in minimal object lock first.
```java

Account acc1 = new Account();
Account acc2 = new Account();

Lock firstLock = acc1.getLock();
Lock SecondLock = acc2.getLock();

if (System.identityHashCode(acc1) < System.identityHashCode(acc2)) {
	firstLock = acc1.getLock();
	secondLock = acc2.getLock();
} else {
	firstLock = acc2.getLock();
	secondLock = acc1.getLock();
}

```

#### **Equals 
- By default, it will check reference both are same or not.
#### **getClass() - (Class object)
- Actually getClass() represent current class. It hold Metadata references(Klass Metadata), Reflection, Serialization are achieved by this Class.
- Execution order,
	1. Object Header has two part first part [[#**Mark Word|Mark word]], Second part Klass pointer(Holds Metadata references).
	2. During class loading Class Metadata creates. It holds Constructor, Fields count.
	3. Based on metadata information object allocates memory into heap.
	4. It normal flow Object klass pointer -> Meta data -> Metaspace.
	5. If, access via java implementation or developer use getClass method to make modification (Jackson's Serialization, Spring Boot's & Tomcat Server Reflections).
#### **Mark Word
- Mark word in object's header, and represent runtime object state.
- It can hold hashCode, Gc log, lock bits. It handle runtime object state efficiently, when, object.hashcode() called, it stores custom hashcode in the mark word( bits 10). When the lightweight lock(Single thread) occur the hashcode copied and stores in stack. it will applicable only the for synchronized block, method, class or lock the object, When heavyweight (Multi thread) hashcode stores in monitor point.
- Bits for mark word,
	1. 01 - normal (unlock)
	2. 10 - Lightweight
	3. 10 - heavyweight
	4. 11 - gc logs
#### **Inner class Rules
- Inner class or Method local class are while compile time it creates separate class file. But Inner class file hold outclass file reference. The reference field creates in compile time and it should be in final.
- Outer class file held instance variables with value, if, inner class use that variable it should be final or effective final. Because of, inner class copied outer class variable's value. If, runtime the value gets updated inner class never known because of it call by value not a reference. The lambda expression also following the same concept, but handles different ways.
#### **Hashmap, LinkedHashMap, HashSet working principles
- By default each 16 buckets are allocates, each buckets can hold unlimited data either linked list or Red-black tree.
- When hash collision happen beyond 8th record or Threshold 0.75 load factor, the buckets under 64 size, it will resize the buckets reaches buckets size until 64. When buckets get resized it generate existing element into rehash  and store it relevant buckets. That's why, Hashmap use find buckets or index based on (n - 1)  & hash. n for size of the buckets existing.
- When collision reaches 64 buckets 8 beyond the buckets records it converts into Red-Black tree for faster getting result. It maintain higher memory so that java uses initially LinkedList and threshold for table in 64 buckets.
- **For concurrency -** If buckets has empty CAS(Compare And Swap) success, just insert and come back. followed insertion request are in synchronized path. The lock only for head of the node. so that another buckets still update. if CAS failed tries until it finishes it work.
- **Node -** both HashMap or hash related all are working same principle the buckets allocation the core logic are same, but their purpose it different and data are different.
- **One point -** LinkedHashMap separated used DoublyLinkedList to maintain orders, rest handles thinks are same in hashmap. 
- **Reference images path -**
	1. ![[internal_working_hashmap_1.png]]
	2. ![[internal_working_hashmap_2.png]]
	3. ![[internal_working_hashmap_3.png]]

#### **Exception
- **Throwable** handles all the errors and exception. it maintains error message, cause of problem, stack traces.
- Throwable 
	- Exception
		- When problem can recoverable is called **Exception.** It may handle by application and application depended all are exceptions.
		- There are two type of Exception:
			1. Checked Exception
				- IOException, FileNotFoundException, SQLException are occur in runtime but the developer should handles these exception it should validate at compile time. 
			2. Unchecked Exception
				- RuntimeException (Unchecked Exception). It validate or unexpected exception it may or not occur.
	- Error
		- **Error** is unrecoverable problems. It system/Jvm aren't recover by application.
#### **Covariant
- A class in is-relationship, both have same method but, object creates in child class reference in parent class. So, parent class reference must return parent method but covariant returns child class methods that is called covariant.
 