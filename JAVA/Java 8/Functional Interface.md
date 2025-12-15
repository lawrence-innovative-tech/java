
#### **Functional Interface
- Interface have only one abstract method and can define variety of implementation to perform a function, but can't modify method parameter.
- Every Interface have abstract methods should be implemented by class. here each abstract method have only one implementation can't reusable different logics.
- But, When if it functional interface wherever can implement abstract method's function based on requirement using lambda and method reference.
- No. of default and static method can create.
- @FunctionalInterface annotation to define the class it functional interface. but not recommended.
#### **Predefined Functional Interfaces

1. [[#**Predefined Functional Interfaces|Predicate Functional Interface]]
2. **Function Functional Interface
3. **Consumer Functional Interface
4. **Supplier Functional Interface 

#### **Predicate Functional Interface
- Predicate is used to test the condition, it's return 'true' or 'false'. 
- It used for filter steams pipeline to optimized approaches. boolean test() used.
- We can combine predicate functional interface between below methods,
	1. default methods for Logical operator functionality.
		1. and() 
		2. or()
		3. negate() - This method is equal to not() method.
	2. static methods
		1. not()
		2. isEqual() - it Perform based on equals() and hashCode()- methods.
- Methods to be used -
	1. filter()
	2. takeWhile()
	3. dropWhile()
	4. allMatch(), anyMatch(), nonMatch().
- **Bi-Predicate**
	- It's allows two condition checks.
	- It have only above default methods.

- **Ref Code -** https://github.com/lawrence-innovative-tech/java-code-review/blob/main/src/main/java/org/example/functionalInterface/predefined/PredicateFunctionalInterface.java
#### **Function Functional Interface
- It convert 'T' generic type to 'R' generic type. And Returns 'R' generic.
- 'T' .apply() method used to change. 'T' type to 'R' type.
- Default methods :
	1. compost() - before process the data.
	2. andThen() - after process the data.
- Static Methods :
	1. identity()   - natural process it return same input as output.
- Stream api methods to be used:
	1. map & co and flatMap & co.
- Bifunction interface perform two input and return the output. Here, there is no static methods only default methods. that is compose() and andThen() methods.

- **Ref Code -** https://github.com/lawrence-innovative-tech/java-code-review/blob/main/src/main/java/org/example/functionalInterface/predefined/FunctionFunctionalInterface.java

#### **Consumer Functional Interface
- Consumer collects data, and process some operation but doesn't returns anything.
- accept() method perform the operation.
- andThen() methods first process current operation followed by after methods.
- Stream methods, peek(), foreach(), foreachOrdered().

#### **Supplier Functional Interface
- Returns output without consuming the inputs. it like opposite of consumer functional interface.
- get() to retrieve data from source, doesn't have default and static methods.
- Streams supplier methods in collect().