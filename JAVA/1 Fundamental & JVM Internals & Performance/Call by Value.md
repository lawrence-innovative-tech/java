
#### **Call by Reference
- When passes to method to execution, their if changes happen of that reference, it would affects the passed variables. Hence, the object-oriented programming has failed.
- Detailed Explain:
  ```java
	int value = 100;
	
	void changeValue(Person newP){
		newP = new Person(); // If it call by reference, here breaks the OOPS concepts.
		newP.value = 100;
	}
	
	Person p = new Person();
	p.value = 10;
	p.changeValue(p);
	
	```
	- Person p = new Person(); // here, java creates object in heap, and assigned object's reference to that p variables or references.
	- I'm passing 'p' object to instance method of Person class.
	- Now, changeValue() method's creates new object and it's stores that object references, If it java in call by reference what newP holds the object reference to be stores in p reference.
	- Here, breaks OOPS concepts. It overcome by [[#**Call by value|Call by value]].
#### **Call by value
- The call by value pass only copy of the reference if it object, copy of the value in primitive types.
- Detailed break down,
```java
	int value = 100;
	
	void changeValue(Person newP){
		newP = new Person(); // Java ueses call by value. so, newP holds new object reference, still p holds old reference.
		newP.value = 100;
	}
	
	Person p = new Person();
	p.value = 10;
	p.changeValue(p);
	```

- And Each stack frames has 

