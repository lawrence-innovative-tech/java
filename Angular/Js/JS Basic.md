
#### **Difference between var, let and Const
- **VAR 
	1. Function scoped, within if, for, and while declared var variable  after the block we can access.
	2. While hoisting it define as undefined.
	3. It allow re declaration, re assignment.
- **LET and CONST
	1.  Both are block variable, so only allowed inside the block.
	2. It also host but it never access until it reaches it declaration.
	3. Let allow to re assign, but not re declaration.
	4. Const never allows re assign and re declaration.
#### **Hoisting
- Before start execution java scan js file allocates memory to declare variables.
#### **Function Reference
- Function reference is assign function declaration into scope. so while hosting only function get allocates memory.
- It throws ReferenceError, only creates object at the execution phase.
``` javascript
greet();  
  
const greet = function() {  
console.log("Hello");  
};
```

#### **Function Declaration
- It creates object for function declaration. not function expression.

``` javascript
sayHello();

function sayHello() {  
  console.log("Hello");
  }
```