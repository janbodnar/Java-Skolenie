# Exceptions

In this article we work with exceptions. Java uses exceptions to handle errors.

During the execution of our application many things might go wrong. A disk might  
get full and we cannot save our data. An Internet connection might go down while  
our application tries to connect to a site. A user fills invalid data to a form.  
These errors can crash the application, make it unresponsive, and in some cases  
even compromise the security of a system. It is a responsibility of a programmer  
to handle errors that can be anticipated.  

In Java we recognize three kinds of exceptions: 

- checked exceptions 
- unchecked exceptions 
- errors

## Checked exceptions

Checked exceptions are error conditions that can be anticipated and recovered  
from (invalid user input, database problems, network outages, absent files). All  
subclasses of `Exception` except for `RuntimeException` and its subclasses are  
checked exceptions. 

`IOException`, `SQLException`, or `PrinterException` are examples of checked  
exceptions. Checked exceptions are forced by Java compiler to be  
either caught or declared in the method signature (using the throws keyword).  

## Unchecked exceptions

Unchecked exceptions are error conditions that cannot be anticipated and  
recovered from. They are usually programming errors and cannot be handled at  
runtime. Unchecked exceptions are subclasses of `java.lang.RuntimeException`.  
`ArithmeticException`, `NullPointerException`, or `BufferOverflowException`  
belong to this group of exceptions. Unchecked exceptions are not enforced by the  
Java compiler.

## Errors

Errors are serious problems that programmers cannot solve. For example hardware  
or system malfunctions cannot be handled by applications. Errors are instances  
of the `java.lang.Error` class. Examples of errors include `InternalError`,  
`OutOfMemoryError`, `StackOverflowError` or `AssertionError`.  

Errors and runtime exceptions are often referred to as unchecked exceptions.  

## The try/catch/finally

The `try`, `catch` and `finally` keywords are used to handle exceptions. The  
`throws` keyword is used in method declarations to specify which exceptions are  
not handled within the method but rather passed to the next higher level of the  
program.  

The `throw` keyword causes the declared exception instance to be thrown. After  
the exception is thrown, the runtime system attempts to find an appropriate  
exception handler. The call stack is a hierarchy of methods that are searched  
for the handler.  

## Unchecked exception examples

Java checked exceptions include: 

- `ArrayIndexOutOfBoundsException`,  
- `UnsupportedOperationException`, 
- `NullPointerException`,  
- `InputMismatchException`.  

## ArrayIndexOutOfBoundsException

`ArrayIndexOutOfBoundsException` is hrown to indicate that an array has been  
accessed with an illegal index. The index is either negative or greater than or  
equal to the size of the array.  

```java
void main() {

    int[] n = { 5, 2, 4, 5, 6, 7, 2 };
    System.out.format("The last element in the array is %d%n", n[n.length]);
}
```

There is a bug in the above program. We try to access an element that does not  
exist. This is a programming error. There is no reason to handle this error: the  
code must be fixed.  

```java
System.out.format("The last element in the array is %d%n", n[n.length]);
```

The array indexes start from zero. Therefore, the last index is `n.length - 1`.



## UnsupportedOperationException

`UnsupportedOperationException` is thrown to indicate that the requested operation  
is not supported.  

```java
import java.util.List;

void main() {

    var words = List.of("sky", "blue", "forest", "lake", "river");
    words.add("ocean");

    System.out.println(words);
}
```

An immutable list is created with `List.of` factory method. The immutable list  
does not support the add method; therefore, we the `UnsupportedOperationException`  
is thrown when we run the example.  

## NullPointerException

`NullPointerException` is thrown when an application attempts to use an object  
reference that has the null value. For instance, we call an instance method on  
the object referred by a null reference.  

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    List<String> words = new ArrayList<>() {{
        add("sky");
        add("blue");
        add("cloud");
        add(null);
        add("ocean");
    }};

    words.forEach(word -> {
        System.out.printf("The %s word has %d letters%n", word, word.length());
    });
}
```

The example loops over a list of strings and determines the length of each of  
the strings. Calling length on a `null` value leads to `NullPointerException`.  
To fix this, we either remove all `null` values from the list of check for a  
`null` value before calling length.    

## InputMismatchException

The `Scanner` class throws an `InputMismatchException` to indicate that the  
token retrieved does not match the pattern for the expected type. This exception  
is an example of an unchecked exception. We are not forced to handle this  
exception by the compiler.  

```java
import java.util.InputMismatchException;
import java.util.Scanner;
import java.util.Locale;
import java.util.logging.Level;
import java.util.logging.Logger;

void main() {

    Locale.setDefault(Locale.ENGLISH);

    System.out.print("Enter an integer: ");

    try {

        try (Scanner sc = new Scanner(System.in)) {

            int x = sc.nextInt();
            System.out.println(x);
        }

    } catch (InputMismatchException e) {

        Logger.getLogger(getClass().getName()).log(Level.SEVERE,
                "wrong data entered");
    }
}
```

The error prone code is placed in the try block. If an exception is thrown, the  
code jumps to the catch block. The exception class that is thrown must match the  
exception following the catch keyword.  

```java
try {

    try (Scanner sc = new Scanner(System.in)) {

        int x = sc.nextInt();
        System.out.println(x);
    }

} 
```

The outer `try` keyword defines a block of statements which can throw an  
exception. The inner `try` is used to release the resources held by `Scanner`.  

```java
} catch (InputMismatchException e) {

    Logger.getLogger(getClass().getName()).log(Level.SEVERE,
            "wrong data entered");
}
```

The exception is handled in the `catch` block. We use the `Logger` class to log  
the error.  

## Checked exceptions

Java checked exceptions include `SQLException`, `IOException`, or `ParseException`.

### SQLException

`SQLException` occurs when working with databases.

```java
package com.zetcode;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.logging.Level;
import java.util.logging.Logger;

public class MySqlVersionEx {

    public static void main(String[] args) {

        Connection con = null;
        Statement st = null;
        ResultSet rs = null;

        String url = "jdbc:mysql://localhost:3306/testdb?useSsl=false";
        String user = "testuser";
        String password = "test623";

        try {

            con = DriverManager.getConnection(url, user, password);
            st = con.createStatement();
            rs = st.executeQuery("SELECT VERSION()");

            if (rs.next()) {

                System.out.println(rs.getString(1));
            }

        } catch (SQLException ex) {

            Logger lgr = Logger.getLogger(MySqlVersionEx.class.getName());
            lgr.log(Level.SEVERE, ex.getMessage(), ex);

        } finally {

            if (rs != null) {
                try {
                    rs.close();
                } catch (SQLException ex) {
                    Logger lgr = Logger.getLogger(MySqlVersionEx.class.getName());
                    lgr.log(Level.SEVERE, ex.getMessage(), ex);
                }
            }

            if (st != null) {
                try {
                    st.close();
                } catch (SQLException ex) {
                    Logger lgr = Logger.getLogger(MySqlVersionEx.class.getName());
                    lgr.log(Level.SEVERE, ex.getMessage(), ex);
                }
            }

            if (con != null) {
                try {
                    con.close();
                } catch (SQLException ex) {
                    Logger lgr = Logger.getLogger(MySqlVersionEx.class.getName());
                    lgr.log(Level.SEVERE, ex.getMessage(), ex);
                }
            }
        }
    }
}
```

The example connects to a MySQL database and finds out the version of the  
database system. Connecting to databases is error prone.  

```java
try {

    con = DriverManager.getConnection(url, user, password);
    st = con.createStatement();
    rs = st.executeQuery("SELECT VERSION()");

    if (rs.next()) {

        System.out.println(rs.getString(1));
    }
}
```

The code that might lead to an error is placed in the `try` block.

```java
} catch (SQLException ex) {

    Logger lgr = Logger.getLogger(Version.class.getName());
    lgr.log(Level.SEVERE, ex.getMessage(), ex);
}
```

When an exception occurs, we jump to the `catch` block. We handle the exception
by logging what happened.  

```java
} finally {

    if (rs != null) {
        try {
            rs.close();
        } catch (SQLException ex) {
            Logger lgr = Logger.getLogger(MySqlVersionEx.class.getName());
            lgr.log(Level.SEVERE, ex.getMessage(), ex);
        }
    }

    if (st != null) {
        try {
            st.close();
        } catch (SQLException ex) {
            Logger lgr = Logger.getLogger(MySqlVersionEx.class.getName());
            lgr.log(Level.SEVERE, ex.getMessage(), ex);
        }
    }

    if (con != null) {
        try {
            con.close();
        } catch (SQLException ex) {
            Logger lgr = Logger.getLogger(MySqlVersionEx.class.getName());
            lgr.log(Level.SEVERE, ex.getMessage(), ex);
        }
    }
}
```

The `finally` block is executed whether we received and exception or not. We are  
trying to close the resources. Even in this process, there might be an  
exception. Therefore, we have other `try/catch` blocks.  

## IOException

`IOException` is thrown when an input/output operation fails. This may be due to  
insufficient permissions or wrong file names.  

```java
package com.zetcode;

import java.io.FileReader;
import java.io.IOException;
import java.nio.charset.StandardCharsets;

public class IOExceptionEx {

    private static FileReader fr;

    public static void main(String[] args) {

        try {

            char[] buf = new char[1024];

            fr = new FileReader("src/resources/data.txt", StandardCharsets.UTF_8);

            while (fr.read(buf) != -1) {

                System.out.println(buf);
            }

        } catch (IOException e) {
            e.printStackTrace();
        } finally {

            if (fr != null) {
                try {
                    fr.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

When we read data from a file, we need to deal with the `IOException`. The  
exception can be thrown when we try to read the data with read and to close the  
reader with close.  

## ParseException

`ParseException` is thrown when a parsing operation fails.

```java
package com.zetcode;

import java.text.NumberFormat;
import java.text.ParseException;
import java.util.Locale;

void main() {

    NumberFormat nf = NumberFormat.getInstance(new Locale("sk", "SK"));
    nf.setMaximumFractionDigits(3);

    try {
        Number num = nf.parse("150000,456");
        System.out.println(num.doubleValue());

    } catch (ParseException e) {
        e.printStackTrace();
    }
}
```

In the example, we parse a localized number value to a Java Number. We handle  
the `ParseException` with `try/catch` statements.

## Throwing exceptions

The `Throwable` class is the superclass of all errors and exceptions in the Java  
language. Only objects that are instances of this class (or one of its  
subclasses) are thrown by the Java Virtual Machine or can be thrown by the Java  
throw statement. Similarly, only this class or one of its subclasses can be the  
argument type in a catch clause.  

Programmers can throw exceptions using the `throw` keyword. Exceptions are often  
handled in a different place from where they are thrown. Methods can throw off  
their responsibility to handle exception by using the throws keyword at the end  
of the method definition. The keyword is followed by comma-separated list of all  
exceptions thrown by that method. Thrown exceptions travel through a call stack  
and look for the closest match.  


```java
import java.util.InputMismatchException;
import java.util.Scanner;
import java.util.logging.Level;
import java.util.logging.Logger;

void main() {

    System.out.print("Enter your age: ");

    try {

        try (Scanner sc = new Scanner(System.in)) {

            short age = sc.nextShort();

            if (age <= 0 || age > 130) {

                throw new IllegalArgumentException("Incorrect age");
            }

            System.out.format("Your age is: %d %n", age);
        }

    } catch (IllegalArgumentException | InputMismatchException e) {

        Logger.getLogger(getClass().getName()).log(Level.SEVERE,
                e.getMessage(), e);
    }
}
```

In the example, we ask the user to enter his age. We read the value and throw an  
exception if the value is outside the range of the expected human age.  

```java
if (age <= 0 || age > 130) {

    throw new IllegalArgumentException("Incorrect age");
}
```

An age cannot be a negative value and there is no record of a person older than  
130 years. If the value is outside of this range we throw a built-in  
`IllegalArgumentException`. This exception is thrown to indicate that a method  
has been passed an illegal or inappropriate argument.  

```java
} catch (IllegalArgumentException | InputMismatchException e) {

        Logger.getLogger(ThrowingExceptions.class.getName()).log(Level.SEVERE,
                e.getMessage(), e);
}
```

It is possible to catch multiple exceptions in one catch clause. However, these  
exceptions cannot be subclasses of each other. For example, `IOException` and  
`FileNotFoundException` cannot be used in one catch statement.  

The following example will show how to pass the responsibility for handling  
exceptions to other methods.  

The `thermopylae.txt` file:

```
The Battle of Thermopylae was fought between an alliance of Greek city-states,  
led by King Leonidas of Sparta, and the Persian Empire of Xerxes I over the  
course of three days, during the second Persian invasion of Greece.  
```

```java
package com.zetcode;

import java.io.BufferedReader;
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public class Main {

    public static void readFileContents(String fname) throws IOException {

        BufferedReader br = null;
        Path myPath = Paths.get(fname);

        try {
            br = Files.newBufferedReader(myPath, StandardCharsets.UTF_8);

            String line;
            while ((line = br.readLine()) != null) {

                System.out.println(line);
            }

        } finally {

            if (br != null) {
                br.close();
            }
        }
    }

    public static void main(String[] args) throws IOException {

        String fileName = "src/main/resources/thermopylae.txt";

        readFileContents(fileName);
    }
}
```

This example reads the contents of a text file. Both `readFileContents` and main  
methods do not handle the potential `IOException`; we let JVM handle it.  

```java
public static void readFileContents(String fname) throws IOException {
```

When we read from a file, an `IOException` can be thrown. The `readFileContents`  
method throws the exception. The task to handle these exceptions is delegated to  
the caller.  

```java
public static void main(String[] args) throws IOException {

    String fileName = "src/main/resources/thermopylae.txt";

    readFileContents(fileName);
}
```

The main method also throws the `IOException`. If there is such an exception, it  
will be handled by JVM.  

## The try-with-resources statement

The try-with-resources statement is a special kind of a try statement. It was  
introduced in Java 7. In parentheses we put one or more resources. These  
resources will be automatically closed at the end of the statement. We do not  
have to manually close the resources.  
  
```java
package com.zetcode;

import java.io.BufferedReader;
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.logging.Level;
import java.util.logging.Logger;

public class Main {

    public static void main(String[] args) {

        String fileName = "src/main/resources/thermopylae.txt";
        Path myPath = Paths.get(fileName);

        try (BufferedReader br = Files.newBufferedReader(myPath,
                StandardCharsets.UTF_8)) {

            String line;
            while ((line = br.readLine()) != null) {

                System.out.println(line);
            }

        } catch (IOException ex) {

            Logger.getLogger(Main.class.getName()).log(Level.SEVERE,
                    ex.getMessage(), ex);
        }
    }
}
```

In the example, we read the contents of a file and use the try-with-resources  
statement.  

```java
try (BufferedReader br = Files.newBufferedReader(myPath,
        StandardCharsets.UTF_8)) {
...
```

An opened file is a resource that must be closed. The resource is placed between  
the square brackets of the try statement. The input stream will be closed  
regardless of whether the try statement completes normally or abruptly.  

## Custom exception

Custom exceptions are user defined exception classes that extend either the  
Exception class or the RuntimeException class. The custom exception is cast off  
with the throw keyword.  

```java
package com.zetcode;

class BigValueException extends Exception {

  public BigValueException(String message) {

        super(message);
    }
}

public class Main {

    public static void main(String[] args) {

        int x = 340004;
        final int LIMIT = 333;

        try {

            if (x > LIMIT) {

                throw new BigValueException("Exceeded the maximum value");
            }

        } catch (BigValueException e) {

            System.out.println(e.getMessage());
        }
    }
}
```

We assume that we have a situation in which we cannot deal with big numbers.  

```java
class BigValueException extends Exception {

  public BigValueException(String message) {

        super(message);
    }
}
```

We have a BigValueException class. This class derives from the built-in  
Exception class. It passes the error message to the parent class using the super  
keyword.  

```java
final int LIMIT = 333;
```

Numbers bigger than this constant are considered to be "big" by our program.  

```java
if (x > LIMIT) {

    throw new BigValueException("Exceeded the maximum value");
}
```

If the value is bigger than the limit, we throw our custom exception. We give  
the exception a message "Exceeded the maximum value".  

```java
} catch (BigValueException e) {

    System.out.println(e.getMessage());
}
```

We `catch` the exception and print its message to the console.
