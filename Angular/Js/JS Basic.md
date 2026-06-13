
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
#### **Function Expression
- Function expression is assign function declaration into scope. so while hosting only function get allocates memory.
- It throws ReferenceError, only creates object at the execution phase.
- Arrow function and function expression are nearly same.
``` javascript
greet();  
  
const funExp = function() {  
console.log("Function expression.");  
};

const arrowFun = () => {
	console.log("This is arrow function.");
}

```

#### **Closure
- The inner function access the outer function scope after completes outer function execution.
- **JavaScript** is call by reference. 
``` javascript
function outer() {
    let name = "John";

    function inner() {
        console.log("Inside inner:", name);
    }

    console.log("Outer is returning inner...");
    return inner;
}

const myClosure = outer();

// Now let's change the value AFTER outer has finished
// (We can't directly change 'name' because it's not accessible, so we'll use another trick)

myClosure();   // First call

// If it was a copy, changing it later wouldn't affect inner.
// But we can prove it's a reference by using an object:
```

- outer() it invoke outer() inside inner function object creates and returns outer function inner function's object reference, it stores myclosure scope.
- Now, myclosure get executes it copied name reference while inner function object creates, so it can used that scope after ends outer scope. This is called closure.
- When outer completes its execution and inner still holds outer scope it possible occur memory leak, so after execution completes reassign null to holding inner object reference so that gc get clear the object. another way while create inner function object with help of **WeakRef** class.
#### **JavaScript Memory Model
-  It uses call stack for method calling, heap for object and array storing. and one more lexical also (will update).  
- It's not like java, slightly different.

### Functions vs Classes — What is the difference?

You said:

> "every function creates object, but access class should creates object, then what is different of it ?"

This is a **very good observation**.

#### In JavaScript:

- **Everything is an object** (almost).
- **Functions are objects** (first-class citizens).
- **Classes are also objects** (syntactic sugar).

Here’s the clear difference:

| Feature      | **Function**                      | **Class**                                       |
| ------------ | --------------------------------- | ----------------------------------------------- |
| Nature       | Regular function                  | Special function (constructor)                  |
| Created with | function or arrow                 | class keyword                                   |
| Usage        | Can be called directly            | Must use new to create instance                 |
| this binding | Depends on how you call it        | Automatically bound to instance                 |
| Prototype    | Has .prototype                    | Has .prototype (under the hood)                 |
| Memory       | One function object               | One constructor + shared prototype              |
| Purpose      | Reusable logic, closures, modules | Blueprint for creating multiple similar objects |

#### Example:

```javascript
// 1. Function (Constructor style - old way)
function Person(name) {
    this.name = name;
}
Person.prototype.sayHello = function() {
    console.log("Hello " + this.name);
};

const p1 = new Person("Alice");   // Creates object
const p2 = new Person("Bob");     // Creates another object

// 2. Class (Modern way - same thing under the hood)
class PersonClass {
    constructor(name) {
        this.name = name;
    }
    sayHello() {
        console.log("Hello " + this.name);
    }
}

const p3 = new PersonClass("Alice");
```

**Key Point**:

- Both Person and PersonClass are **functions** internally.
- class is just cleaner syntax.
- When you do new Person(), JavaScript creates a new object and links its __proto__ to Person.prototype.

#### **Arrow Function and Normal Function
- **Arrow Function** is shorter way to declare function. The normal function use this current context or object. But, the arrow function determined from surrounded lexical scope for this.
- It used to define asynchronous process.

#### **Promise
- Promise is eventual completion or failure of an asynchronous process. It return values.
- then() is process success from promise returns.
#### **async & await
- When a function define as async keyword it process asynchronously and return promise.
- Await, it used to hold function until promise to complete.

#### **Event Loop
- JavaScript is Single thread concept, But web api need to process asynchronous operations. 
- 