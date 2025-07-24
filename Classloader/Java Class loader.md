### Introduction

A class loader is an object to load a java classes and it's a part of the JRE. It never create object of the class instead it loads the class into memory especially required classes.

### Main function of the loaders

Two main function
	1. Load the classes - It load the java classes (build-in or custom). We can extend the  **Class Loader** abstract class to implement.
	2. Locate the Resources - A resource the such as .class, image, configuration information, application or library. It based load packages.

### Type of the Loaders

Basically, three type of the loader are exist. But in my point view there is a four. Because the last one is not a loader instead it load the primitive data type and array so that I declare as is loader.

1. Bootstrap Class Loader : 
2. Platform Class Loader :
3. Application or System Class Loader : 
4. JRE - It loads only **Primitive data types and array**.