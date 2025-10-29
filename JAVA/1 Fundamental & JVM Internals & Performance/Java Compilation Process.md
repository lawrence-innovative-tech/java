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
- After generated token, It will create the AST, It's intermediate for further processing.
- 