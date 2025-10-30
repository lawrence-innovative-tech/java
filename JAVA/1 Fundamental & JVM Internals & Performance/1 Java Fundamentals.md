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
#### **JRE (Java Runtime Environment)
- 


#### **Byte Code 
- Binary code is low machine read & executable code, in 0's and 1's format.
### **JVM Internals & Performance 


#### **Question Bank
1. JDK is enough to create jar file then what is the purpose of Maven the build tool and some plugins in needs to build jar why?
2. The java packages are in JRE we are using java api to our application, so where it can load and how its represented in .class file.
3. Semantic analysis will checks global variable's default value is optional, but local variable's default value should be present. why?