
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
	1. compose() - before process the data. First parameter get execute after instance get executes.
	2. andThen() - after process the data. First instance get executes after parameter that get executes.
- Static Methods :
	1. identity()   - natural process it return same input as output.
- Stream api methods to be used:
	1. map & co and flatMap & co.
- Bifunction interface perform two input and return the output. Here, there is no static methods only default methods. that is compose() and andThen() methods.
- Edge Cases: If the stream is empty, only the supplier is called (followed by the finisher). For parallel streams, multiple suppliers may be invoked (one per thread).

- **Ref Code -** https://github.com/lawrence-innovative-tech/java-code-review/blob/main/src/main/java/org/example/functionalInterface/predefined/FunctionFunctionalInterface.java

#### **Consumer Functional Interface
- Consumer collects data, and process some operation but doesn't returns anything.
- accept() method perform the operation.
- andThen() methods first process current operation followed by after methods.
- Stream methods, peek(), foreach(), foreachOrdered().
- The collector interface have accumulator in Bi-Consumer Functional Interface.
- Edge Cases: In parallel streams, the same container might be updated concurrently, so avoid non-atomic operations like simple increments unless using CONCURRENT. It's the most frequently called method, so optimize for performance.

#### **Supplier Functional Interface
- Returns output without consuming the inputs. it like opposite of consumer functional interface.
- get() to retrieve data from source, doesn't have default and static methods.
- Streams supplier methods in collect().
- Edge Cases: If the stream is empty, only the supplier is called (followed by the finisher). For parallel streams, multiple suppliers may be invoked (one per thread).

#### **Binary Operator Functional Interface
- Combine two result set into single result set, It's often call parallel stream processing, but ideal in sequential processing.
- Mostly it used to merge the result set.
- Edge Cases: In fully parallel execution, combiners form a reduction tree (like a tournament). If the collector is UNORDERED, the merge order doesn't matter. For non-associative ops, results may vary across runs.

#### **Finisher Functional Interface
- The return function transform mutable result into immutable result set.
- Edge Cases: For empty streams, it's still called on the empty container from supplier. Keep it lightweight, as it's a post-processing step.