# Lexical structure

Computer languages, like human languages, have a lexical structure. A source  
code of a Java program consists of tokens. Tokens are atomic code elements. In  
Java we have comments, identifiers, literals, operators, separators, and  
keywords.  

Java programs are composed of characters from the Unicode character set.  

# Comments

Comments are used by humans to clarify source code. There are three types of  
comments in Java:  

| Comment type | Meaning |
| --- | --- |
| `// comment` | Single-line comments |
| `/* comment */` | Multi-line comments |
| `/** documentation */` | Documentation comments |

If we want to add some small comment we can use single-line comments. For more  
complicated explanations, we can use multi-line comments. The documentation  
comments are used to prepare automatically generated documentation. This is  
generated with the javadoc tool.  

```java
package com.zetcode;

/*
  This is Comments.java 
  Author: Jan Bodnar
  ZetCode 2024
*/

public class Comments {

    // Program starts here
    public static void main(String[] args) {

        System.out.println("This is Comments.java");
    }
}
```

The program uses two types of comments.

```java
// Program starts here
```

This is an example of a single-line comment.

Comments are ignored by the Java compiler.

```java
/*
  This is Comments.java 
/*  Author: Jan Bodnar */
  ZetCode 2022
*/
```

Comments cannot be nested. The above code does not compile.

## White space

White space in Java is used to separate tokens in the source file. It is also  
used to improve readability of the source code.  

```java
int i = 0;
```

White spaces are required in some places. For example between the int keyword  
and the variable name. In other places, white spaces are forbidden. They cannot  
be present in variable identifiers or language keywords.  

```java
int a=1;
int b = 2;
int c  =  3;
```

The amount of space put between tokens is irrelevant for the Java compiler. The  
white space should be used consistently in Java source code.  

## Identifiers

Identifiers are names for variables, methods, classes, or parameters.  
Identifiers can have alphanumerical characters, underscores and dollar signs  
($). It is an error to begin a variable name with a number. White space in names  
is not permitted.  

Identifiers are case sensitive. This means that `Name`, `name`, or `NAME` refer  
to three different variables. Identifiers also cannot match language keywords.   

There are also conventions related to naming of identifiers. The names should be  
descriptive. We should not use cryptic names for our identifiers. If the name  
consists of multiple words, each subsequent word is capitalized.  

```java
String name23;
int _col;
short car_age;
```

These are valid Java identifiers.

```java
String 23name;
int %col;
short car age;
```

These are invalid Java identifiers.

The following program demonstrates that the variable names are case sensitive.  
Event though the language permits this, it is not a recommended practice to do.  

```java
void main() {
        
    String name = "Robert";
    String Name = "Julia";

    System.out.println(name);
    System.out.println(Name);
}
```

`Name` and `name` are two different identifiers. In Visual Basic, this would not  
be possible. In this language, variable names are not case sensitive.  

---

A literal is a textual representation of a particular value of a type. Literal  
types include boolean, integer, floating point, string, null, or character.  
Technically, a literal will be assigned a value at compile time, while a  
variable will be assigned at runtime.  

```java
int age = 29;
String nationality = "Hungarian";
```

Here we assign two literals to variables. Number 29 and string "Hungarian" are
literals.  

```java
void main() {

    int age = 23;
    String name = "James";
    boolean sng = true;
    String job = null;
    double weight = 68.5;
    char c = 'J';

    System.out.format("His name is %s%n", name);
    System.out.format("His is %d years old%n", age);

    if (sng) {
        
        System.out.println("He is single");
    } else {
        
        System.out.println("He is in a relationship");
    }

    System.out.format("His job is %s%n", job);
    System.out.format("He weighs %f kilograms%n", weight);
    System.out.format("His name begins with %c%n", c);
}
```

In the above example, we have several literal values. 23 is an integer literal.  
"James" is a string literal. The true is a boolean literal. The null is a  
literal that represents a missing value. 68.5 is a floating point literal. 'J'  
is a character literal.  


## Operators

An operator is a symbol used to perform an action on some value. Operators are  
used in expressions to describe operations involving one or more operands.  

```
+    -    *    /    %    ^    &    |    !    ~
=    +=   -=   *=   /=   %=    ^=    ++    --
==   !=    <   >    &=  >>=   <<=   >=   <= 
||   &&    >>    <<    ?:
```

This is a partial list of Java operators. 

## Separators 

A separator is a sequence of one or more characters used to specify the boundary  
between separate, independent regions in plain text or other data stream.    

```
[ ]   ( )   { }   ,   ;   .   "
```

```java
String language = "Java";
```

The double quotes are used to mark the beginning and the end of a string. The  
semicolon ; character is used to end each Java statement.  

```java
System.out.println("Java language");
```

Parentheses (round brackets) always follow a method name. Between the  
parentheses we declare the input parameters. The parentheses are present even if  
the method does not take any parameters. The `System.out.println` method takes one  
parameter, a string value. The dot character separates the class name (`System`)  
from the member (`out`) and the member from the method name (`println`).  

```java
int[] array = new int[5] { 1, 2, 3, 4, 5 };
```

The square brackets `[]` are used to denote an array type. They are also used to  
access or modify array elements. The curly brackets `{}` are used to initiate  
arrays. The curly brackets are also used enclose the body of a method or a  
class.  

```java
int a, b, c;
```

The comma character separates variables in a single declaration.  

## Keywords

A keyword is a reserved word in Java language. Keywords are used to perform a  
specific task in the computer program. For example, to define variables, do  
repetitive tasks or perform logical operations.  

Java is rich in keywords. Many of them will be explained in this tutorial.  

```
abstract        continue        for             new             switch 
assert          default         goto            package         synchronized
boolean         do              if              private         this
break           double          implements      protected       throw
byte            else            import          public          throws
case            enum            instanceof      return          transient
catch           extends         int             short           try
char            final           interface       static          var 
class           finally         long            strictfp        void 
const           float           native          super           volatile
                                                                while
```

In the following small program, we use several Java keywords.

```java
package com.zetcode;

public class Keywords {

    public static void main(String[] args) {

        for (int i = 0; i <= 5; i++) {
            
            System.out.println(i);
        }
    }
}
```

The `package`, `public`, `class`, `static`, `void`, `int`, `for` tokens are Java
keywords.

## Java conventions

Conventions are best practices followed by programmers when writing source code.  
Each language can have its own set of conventions. Conventions are not strict  
rules; they are merely recommendations for writing good quality code. We mention  
a few conventions that are recognized by Java programmers. (And often by other  
programmers too).  

- Class names begin with an uppercase letter.
- Method names begin with a lowercase letter.
- The public keyword precedes the static keyword when both are used.
- The parameter name of the main method is called args.
- Constants are written in uppercase.
- Each subsequent word in an identifier name begins with a capital letter.
