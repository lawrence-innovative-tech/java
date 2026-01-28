
#### **Generics 
- The important think of generics is **Type Safety** to avoid **ClassCastException**, this validate at compile time, runtime happens in erasure.
- Generic is a different class or classes can reusable the same resource.
- The validation happen in compile time, after compilation done, it become a raw type, here happen erasure.
	- e.g. List\<String> becomes list in runtime, after semantics validates the type it start to change erasure.
	- SpringBoot JPA  & @RequestBody can handles **Spring Jackson json deserialization validate methods parameter directly using reflection.** because during compilation erasure happens this change generic type to raw or Object.
- T E K V N - these are generic name
	- T - Type Reference
	- E - element 
	- K - key
	- V - Value
	- N - number
	- S - Supplier
	- ? - Unknown Reference (Wildcard)
#### **Key benefits:

- **Type Safety**: Ensures only compatible types are used, reducing bugs.
- **Code Reusability**: Write once, use with any type (e.g., List\<Integer> vs. List\<String>).
- **Eliminate Casting**: No need for explicit casts, improving readability.
- **Better IDE Support**: Autocompletion and refactoring work seamlessly.
- Generic bound using PESC (Producer Extends, Super Consumer).

- There are two type generic,
	1. Bound Type Parameter
		1. [[#Upper Bound Type Parameter (Producer Extends)|Upper Bound Type Parameter (Producer Extends)]]
		2. [[#Lower Bound Type Parameter (Super Consumer)|Lower Bound Type Parameter (Super Consumer)]]
	2. Unbound Type Parameter (?)
#### **Upper Bound Type Parameter (Producer Extends)
- \<? extends T> ? representation to class.
	- T representation class. which are classes extends T only allows.
	- A class is extends T, so a class is subclass, each subclass vary from other subclasses, so that only allow to read. 
	- It restrict to write and only allows null.
	- 
#### **Lower Bound Type Parameter (Super Consumer)
- \<? super T> ? representation to class.
	- T class or T class's super can allow to write data. so, that other subclass can use that without ClassCastException. When parent class are inherited by child classes so there also create by problems. 
	- We can add subclasses also.