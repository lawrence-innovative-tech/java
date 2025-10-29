#### **1. Lexical Analysis (Tokenization)
- Reads a source (.java) file and stores into **char[] buffer** to generate the [[#Tokenization|Token]].
- It's breaks code into stream of tokens such as **Keywords (Public, class, static), identifiers (variable name, sout), literal (integer literal, string literal), Symbols ({,;).
- Here removes the whitespace and command parts.
- When non-matched keywords are throw lexical error.

**Notes**
- The Scanner class is used to generate Tokens.
#### Tokenization 
- Reads high level programming the java code in character-by-character frame token streams.
	- e.x Sample token Generation code
``` java
import java.io.*;  
import com.sun.tools.javac.parser.Scanner;  
import com.sun.tools.javac.parser.ScannerFactory;  
import com.sun.tools.javac.util.Context;  
import com.sun.tools.javac.util.Log;  
import com.sun.tools.javac.util.Options;  
import com.sun.tools.javac.main.JavaCompiler;  
import com.sun.tools.javac.tree.JCTree;  
  
public class TokenPrinter {  
    public static void main(String[] args) throws IOException {  
        // Hardcoded example code (or read from file)  
        String sourceCode = "  
            public class Hello {                
			    public static void main(String[] args) {  
				    System.out.println("Hello, Tokens!");                    
		            int a = 500;                    
		            System.out.println(a);                    
			        static class innerClass {                        
				        System.out.println("Inner class");                    
				    }
				    TokenPrinter tp = new TokenPrinter();                              
			    }  
            }";  
  
        // Setup javac context (internal, but safe)  
        Context context = new Context();  
        Options.instance(context).put("nowarn", "true");  
        Log.instance(context);  
  
        // Create scanner (lexer)  
        ScannerFactory scannerFactory = ScannerFactory.instance(context);  
        Scanner scanner = scannerFactory.newScanner(sourceCode, false);  
  
        // Print tokens  
        System.out.println("Token Stream:");  
        System.out.println("=============");  
        scanner.nextToken(); // Prime it  
        while (scanner.token().kind.name() != "EOF") {  
            System.out.println(scanner.token().kind + " : " + scanner.token() + " 
	            : " + scanner.token().kind.name() + " : " +  
                    scanner.token().pos + " : " + scanner.token().pos + " : " + 
                    scanner.token().deprecatedFlag() );  
            scanner.nextToken();  
        }  
        System.out.println("EOF (End of File)");  
        System.out.println("- "+Character.isLetterOrDigit(4));  
    }  
}
```

#### **2. Syntax Analysis (AST - Abstract Syntax Tree)
- After generated token, It will create the AST for code structure in hierarchical representation, and AST an intermediator of following process.
- While build the AST to know the compiler in syntax error, like missing semicolon, unbalanced parentheses.
#### **3. Semantic Analysis (Logical Validation)
- The complier complete generation of AST, it will start process to validate logic or purpose of the application.
- It will traverse the AST tree to check the flow of logic.
	- **Symbol Resolution -** It identify the reference, which imported or external libraries.
	- **Type Checking -** It will check type compatible.
		 1. int store only integer value not string value
		 2. ParentClass object = new ChildClass();
			- object.test();
			 - Here, child class one method which not in parent class but the object creating for child class in runtime, but compile time which check only parent class.
	- **Flow Checking -** it find out unreachable code, uninitialized variables, or definite assignment rules.
- Here, the code get optimization like, when we call static variable using this or object reference it update the AST in relevant class name.
- If code has annotation, here checks and implemented the annotation functionality like (Lombok).
#### **4. Byte Code Generation
- 