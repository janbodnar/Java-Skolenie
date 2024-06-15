# Packages

A *package* is a grouping of related types providing access protection and name  
space management. Packages in Java is a similar concept to namespaces in C#.  


A package is declared with the `package` keyword. This statement must be placed  
at the top of every source file. There can be only one such statement in each  
source file. The Java source files must be placed in directories that match the  
package name.  

```java
package com.zetcode;
```

All types defined in the file with the above package are part of the  
`com.zetcode` package. A class Being has a fully qualified name  
`com.zetcode.Being`.

There are millions of Java programmers worldwide. To avoid potential name  
conflicts, there is a naming convention in Java. The package names use reversed  
Internet domain names. The letters are written in lowercase. There can be only  
one `zetcode.com` domain name so using a reversed name `com.zetcode` for the  
packages will make them unique. A Java source file with a `com.zetcode` package  
must be located in the `com/zetcode` subdirectory. Package names are written in  
all lower case to avoid conflict with the names of classes or interfaces.  

The `import` keyword is used at the beginning of a source file to specify types  
(classes, interfaces, enumerations, or annotations) or entire Java packages to  
be referred to later without including their package names in the reference.  
Import statements can import static members of a class (methods and variables).  

```java
import java.awt.*;
```

Using the `*` wildcard character, we can import the whole package at a time.  
After this import, we can refer to all types of the java.awt package without  
their fully qualified names.  

```java
import java.awt.event.*;
```

The `java.awt.event` subpackage is not imported with the `java.awt.*` import.  
Subpackages must be imported independently.  

```java
import java.util.Random;
```

In this case, only `Random` class is imported. Now the `Random` class can be  
referenced using its simple class name.  

## Core packages in Java

The following is a partial list of core packages in Java:

- java.lang — basic language functionality and fundamental types  
- java.util — collection data structure classes  
- java.io — Java API for file operations  
- java.math — multiprecision arithmetics  
- java.nio — the Non-blocking I/O framework for Java  
- java.net — networking operations, sockets, DNS lookups, ...  
- java.security — key generation, encryption and decryption  
- java.sql — Java Database Connectivity (JDBC) to access databases  
- java.awt — basic hierarchy of packages for native GUI components  
- javax.swing — hierarchy of packages for platform-independent rich GUI components  
- java.beans — Contains classes related to developing beans --  
   components based on the JavaBean architecture.  
- java.text — Provides classes and interfaces for handling text, dates,  
   numbers, and messages in a manner independent of natural languages.  
- java.rmi — Java API for remote method invocations.  
- java.time — The main API for dates, times, instants, and durations.  
- The java.lang package is available without the use of an import statement.  

## Practical example

The following example shows how to create a package and import types.  

```java
package com.zetcode;

import java.util.Random;

// com/zetcode/Packages.java
public class Packages {

    public static void main(String[] args) {

        var r = new Random();

        int x = r.nextInt();
        System.out.println(x);

        java.time.LocalDateTime dt = java.time.LocalDateTime.now();
        System.out.println(dt);
    }
}
```

The example uses two types: the `Random` class and the `LocalDateTime` class.  
The first class is imported and the second is referred by its fully qualified  
name.

```java
package com.zetcode;
```

We declare a package with the `package` keyword. The `Packages.java` file must  
be located in the `com/zetcode` subdirectory.

```java
import java.util.Random;
```

This code line enables us to use the `Random` class without the package name.  

```java
var r = new Random();
```

Here we use the `Random` without using its full name.

```java
java.time.LocalDateTime dt = java.time.LocalDateTime.now();
```

If we did not use the import keyword on a type, we can refer to it only by its  
full name - `java.time.LocalDateTime` in our case. The `import` keyword saves a  
lot of typing.



# The package-private visibility

If we do not specify any access modifier (e.g. private, protected, or public),  
we have a package-private visibility. In such a case, variables and methods are  
accessible within the same package. Classes in other packages cannot access  
classes and members declared with package-private access.  

## The default package

If no package is declared, all types defined in that file are part of a default  
unnamed package. It is recommended to always place your types in a package. Even  
for small programs.  

```java
public class DefaultPackage {

    public static void main(String[] args) {

        System.out.println("A class in a default package");
    }
}
```

The `DefaultPackage` class is part of the default package.

## Automatic imports

Java compiler automatically imports two packages: `java.lang` and the current  
package.  

```java
package com.zetcode;

// com/zetcode/Constants.java
public class Constants {

    public static final String version = "1.0";
}
```

The `Constants` class is located in the same package as the `AutomaticImports`  
which is referring to its version member.

```java
package com.zetcode;

// com/zetcode/AutomaticImports.java
public class AutomaticImports {

    public static void main(String[] args) {

        String os = System.getProperty("os.name");

        System.out.println(os);
        System.out.println(Constants.version);
    }
}
```

In this example, we refer to some classes that are automatically imported by  
Java compiler.  

```java
String os = System.getProperty("os.name");
```

The `String` and `System` classes are part of the `java.lang` package.  

```java
System.out.println(Constants.version);
```

The `Constants` class is located in the same package as the `AutomaticImports`  
class. Therefore, we can access the class and its member without using the fully  
qualified name or utilizing the `import` keyword.

## Static imports

If we often use some static members, we can use import static statement to refer  
to them later without a full class name. Static imports should be used with  
caution.  

```java
package com.zetcode;

import static java.lang.Math.E;
import static java.lang.Math.PI;
import static java.lang.Math.abs;

public class StaticImport {

    public static void main(String[] args) {

        System.out.println(E);
        System.out.println(PI);

        System.out.println(abs(-5));
    }
}
```

In this example, we refer to two constants and one static method.

```java
import static java.lang.Math.E;
import static java.lang.Math.PI;
import static java.lang.Math.abs;
```

We use the `import static` statement to enable referring to them without their  
full names.  

```java
System.out.println(E);
System.out.println(PI);
```

```java
System.out.println(abs(-5));
```

We refer to these three members without their class name.
