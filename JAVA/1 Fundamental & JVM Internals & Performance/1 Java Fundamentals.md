###### **Ref -** https://docs.oracle.com/javase/specs/jls/se7/html/jls-12.html
###### **Ref of Medium -** https://medium.com/platform-engineer/understanding-jvm-architecture-22c0ddf09722
### **What is JAVA 

	Java is high level, Objexct-Oriented programming language, and Platform developed by SUN MicroSystem in 1995 (Now owned by Orcle).

### **Features of Java
	1. Platform Independent : Build or Write once and Run anywhere(WORA).
	2. Object-Oriented : Everything in java resolves around classes and obejects.
	3. MultiThreading : Java has special feature to handle multithreading.
	4. Automatic GC : Java handles the memory management, Using GC.
	5. Robust Application : Handles unexcepted exception like running out of memory, wrong input.
		1. Bigest Robust: Memeory management.
		2. Strict compile time checking : 
		   Strickly typed - Compiler knowns type of variables and expression in compile time. 
		Strongly typed - Compiler enforces to type constraints which means String type    operation could not perform to Integer. 
				ex. 
					String name = "Alice";
					int length = name.length(); // Correct
					int result = name * 5; // COMPILE-TIME ERROR: The operator * is undefined for String, int
	6. Security : Java has multiple security level.

### **Architecture of Java 

``` java
Source code (.java) // Java file
	↓
Java Compiler (Javac) // Done by JDK
	↓
ByteCode Conversation // JDK part (For Platform Independent)
	↓
JVM (Java Virtual Machine) // Platform Specific to convert(bytecode to binary code) & execute.
	↓
Native Machine Code // Binary code (0's & 1's)
	↓
Execution
```

#### **JDK, JRE and JVM

#### **JDK ( Java Development Kit )

- JDK is cross platform Software Development tool to building a java application. it's a Kit ( or a Package), it contains all the necessary to build and executable java tools, libraries, compile, debug, and run. Without JDK, We can't create a new think but we can use precompiled using JRE.
- JDK contains [[#**JDK TOOLS | JDK TOOLS]] + [[#**JRE (Java Runtime Environment)|JRE]].

##### **JDK TOOLS
- javac (Java Compiler ) - Convert human readable ( High level language ) to Machine or java executable ( Low level language [[#**Byte Code|ByteCode]]), without javac tool we can't convert executable format. for more [[Java Compilation Process|clarity]].
- javadoc - Generate Java documentations
- jvisualvm - Analysis the performance.
- javap - we can see JVM instruction in high-level. (e.x javap -c <class_name>, javap -v (Full overview)).
- javac -Xprint flag - to print java code in console for highlevel.
- Module-info.java its for only necessary package to compile and run application.

#### **JRE (Java Runtime Environment)
- JRE contains JVM + Libraries, the execution are happens in JVM, but all necessary package are supplies from JRE.
- In Simple word, JRE is car, JVM is engine. so, without tyre car can't move.
- **JVM Works
	1. When "JAVA <CLASS_NAME>" instruction given from user it's loads the <CLASS_NAME> from respective path.
	2. And, Initiate the JVM to start process.
- JRE has jvm's binary libes.
- Module means its minimal JRE to run our application, which means it will have only necessary package to use to run application.
- To run application using jlink command with [[#**Module|module-info.java]] path.

#### **Module
 - Module from Java 9 and 9+.
 - **Before Java 9 -** JRE is loads all the jar which in rt.jar.
 - **From Java 9 -** Java introduced Module for required dependency and control the package, jars, with encapsulate.
	 1. Module-info.java - It's a file its contains below context.
	 2. required - Here, we can mention what are the packages to be needs to run this application.
	 3. exports - What are packages to be expose to other packages has access this package.
	 4. open - It's allow reflection access (like spring framework and JSON libs).
	 5. uses / provides - For service loading (advanced).
``` java
myapp/
├── com/
│   └── example/
│       └── Greeting.java
└── module-info.java
```

``` java
module com.example.myapp {
    exports com.example;        // Allow others to use com.example package
    requires java.base;         // Automatically added by compiler (optional)
}

// Compile Command
javac -d mods/com.example.myapp \
    src/com.example.myapp/com/example/Greeting.java \
    src/com.example.myapp/module-info.java
    
// Run Command
java --module-path mods \
     --module com.example.myapp/com.example.Main
```

- **Ref -** https://grok.com/c/4c1cae52-93e8-4440-8da4-c1d48e3ccabf

#### **Byte Code 
- Binary code is JVM instruction code. The class have all the details about memory allocation, object allocation, variables insertion and assignment and all the information regarding the class.
### **JVM Internals & Performance 
1. JVM is core component of executes the java code which contains,
	1. Loader (Class loader) 
	2. Linking
	3. Initializer
	4. Execution (Interpreter & JIT)
	5. GC (Garbage Collection)
2. **Loading -**
	1. When java launcher triggered, the JRE start to execute java code, Initially its call jvm.dl to initiated JVM.
	2. JVM start loads .classfile using [[Java Class loader#**Class Loaders|loaders]] to load bytecode to [[Memory Model#**Method Area|method area]]. 
	3. Then Creates class object of that class. [[#**Class object for loading period|Explanation of that object]].
	4. After creates the object, Loading instruct to method area to assigned the object to be addressed there.
	5. After loading part completed, it will trigger to linking. Up to linking it must be execute.
	6. When loading, linking has completed there is no error without initialized. // **Update later.
3. **Linking -** When loading completes it initiate to start process of linking. Here,
	1. **Verification -** To verify the bytecode the of class, If verification failed, throw verify error.
		- Checks the malformed bytecode are present or not, virus checks.
	2. **Preparation -** In this case, To loads a static variables with default values in method area.
	3. **Resolution -** If class has referenced symbols like extends another class, implemented interface, Declaration of another class from jar, dependency and etc. It's process recursively (the new Loading -> Linking -> Init.. to that parent class).
		1. When resolution triggers it executes up to initialization, after child class's initialization followed by object creation, here parent class block and constructor get run first. because if child can reallocates based on parent class that is concept of inheritance.
4. **Initialization -** Here, 
	- It will assign loaded static variables if that variables has values. And then, initiate to Object creation using '\<clinit>'.
	- First static variables assign and then static methods and static blocks..
5. **Execution** 
	- It will creates object in Eden space, if it full, then stores in old generation part. (More details in Memory Model).
	- Initially, Instance variables has default with, If class have parent call **super()** method to setup parent class fields and methods/constructor.
	- After parent loaded the assigned value get initialized to that variables after that instance Block get execution. followed by constructor (applicable for parent class also).
	- how first parent completes for static fields same as object creation child linked with parent.
6. **Interpreter** (TODO Details later)
	- Initially interpreter has started to process the instruction.
	- Interpreter checks the value before to use like NullPointerException.
	- It's slow to process the instruction like, e.g. int a = 5;
		- First initially push 'a' to stack.
		- Then, pop the 'a' assigned 5.
		- Again push to 'a = 5' stack.
		- But, JIT compiler learn the frequently use process and skips unreached and wanted steps.
7. **JIT (Just-In-Time) -  (TODO Details later)
	- 
#### **Class object for loading period
- creates the object for that class (This not a user created object instead it's a loaded class's class object. Which is used to create user object and link between method area to address the code, methods, and necessary thinks. 
	- This only one to generates for the class, but user can create multiple object using this object (The object initial first 6 bytes refer to class object for fast accessing to method area).
	- If different loaders load same class the object in duplicate, the address object like this 
	  loader + class name so that when single loaders the object should in identical instead different loader load the same class definitely the object in duplicate.
- The object memory allocation in heap, runs constuctors 
#### **Question Bank for Learning
1. JDK is enough to create jar file then what is the purpose of Maven the build tool and some plugins in needs to build jar why?
2. The java packages are in JRE we are using java api to our application, so where it can load and how its represented in .class file.
3. Semantic analysis will checks global variable's default value is optional, but local variable's default value should be present. why?

#### **Question Bank for  Learned Topics
1. **Can we load same class twice to JVM?
	- Yes, It's possible because **JVM architecture is isolates class for their class loader boundaries.** 
	- Tomcat web server have Test.war and Test.war1 but both war file's classes in identical. But each war file has different Classloader. so, JVM consider both are different application so its load. (Tomcat provides each war have its own Classloader). 
	- **Spring DevTools also using the classloader in different purposes. It's should be Update in Spring Learning Part. 
2. **Why is String.class loaded by the Bootstrap loader even before main()?
	- When a user passes some commands through command-line arguments its stores and process as needed places. The command format is "String". 
	- JVM loads below classes.
		1. `java.lang.Object`
		2. `java.lang.Class`
		3. `java.lang.String`
		4. `java.lang.System`
		5. `java.lang.Thread`
		6. `java.lang.Throwable`
		7. `java.lang.Error`
		8. `java.lang.Exception`
		9. `java.lang.Integer`, `Long`, `Double` (basic wrappers)
		10. `java.lang.StringBuilder` / `StringBuffer`
