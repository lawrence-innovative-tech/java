
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
- Generic bound using PESC (Producer Extends, Super Consumer).
- There are two type generic,
	1. Bound Type Parameter
		1. [[#Upper Bound Type Parameter (Producer Extends)|Upper Bound Type Parameter (Producer Extends)]]
		2. Lower Bound Type Parameter (Super Consumer)
	2. Unbound Type Parameter (?)
#### **Upper Bound Type Parameter (Producer Extends)
