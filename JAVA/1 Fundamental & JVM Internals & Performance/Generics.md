
#### **Generics 
- Generic is a different class or classes can reusable the same resource.
- The validation happen in compile time, after compilation done, it become a raw type, here happen erasure.
	- e.g. List\<String> becomes list in runtime, after semantics validates the type it start to change erasure.
	- Springboot JPA  & @RequestBody can handles **Spring Jackson json deserialization validate methods parameter directly using reflection.** because during compilation erasure happens this change generic type to raw or Object.
- T E K V N - these are generic name
	- E - element 
	- K - key
	- V - Value
	- N - number
	- S - Supplier
- Generic bound using PESC (Producer Extends, Super Consumer).
- There are two type generic,
	1. Bound Type Parameter
		1. [[#Upper Bound Type Parameter (Producer Extends)|Upper Bound Type Parameter (Producer Extends)]]
		2. [[#Lower Bound Type Parameter (Super Consumer)|Lower Bound Type Parameter (Super Consumer)]]
	2. Unbound Type Parameter (?)
#### **Upper Bound Type Parameter (Producer Extends)
- \<? extends TinyUrl> ? representation to class.
	- A class is extends the TinyUrl, so a class representation is subclass, each subclass vary from other, so here allowed only to read. 
#### **Lower Bound Type Parameter (Super Consumer)
- \<? super TinyUrl> ? representation to class.
	- A class's super class is TinyUrl, so that under the TinyUrl we can add all the sub classes to that list. it allows to write.