### Introduction

A class loader is an object to load a java classes and it's a part of the JRE. It never create object of the class instead it loads the class into memory especially required classes.

#### **Class Loaders
 - Class loader is initial step of execution process of reads all the bytecode of the class.
 - There are major three type of loader. which is, 
	 1. Bootstrap (Parent of Extension)
	 2. Platform or Extension (Parent of Application)
	 3. Application or System class loaders.
	 4. The fourth Custom loader which is handle by user. (e.g. Tomcat server, SpringBoot).
- The class loaders are depends on the parent loaders, When loading has initiate from JVM the loader search the path and get loads the class loaders. So, if application loaders not found then pass it to platform loaders, if platform loader not found it will pass to bootstrap loaders. Similarly, bootstrap not found the class it will through **ClassNotException**. 

### Main function of the loaders

Two main function
	1. Load the classes - It load the java classes (build-in or custom). We can extend the  **Class Loader** abstract class to implement.
	2. Locate the Resources - A resource the such as .class, image, configuration information, application or library. It based load packages.

### Type of the Loaders

Basically, three type of the loader are exist. But in my point view there is a four. Because the last one is not a loader instead it load the primitive data type and array so that I declare as is loader.

1. Bootstrap Class Loader : Loads all the necessary JDK classes which are used in the application.
		and it's written by C/C++ and it have own search path.  And it's part of the JVM so it loads the necessary JDK classes.
2. Platform Class Loader or Extension Class Loader : It's help load subclass of the <JAVA_HOME>/lib/ext.
3. Application or System Class Loader : 
4. JRE - It loads only **Primitive data types and array**. 

![[JavaClassLoader-Architecture.webp]]