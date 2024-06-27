# Annotations

Annotations are a special kind of code element that provides additional  
information about a program. They are attached to classes, methods, fields, and  
other program elements using the `@` symbol. 


Annotations themselves don't directly affect how the code runs, but instead  
provide metadata that can be used by various tools:  

* **Compiler:** The compiler can use annotations to check for errors or suppress  
  warnings during compilation. For instance, the `@Override` annotation tells  
  the compiler to verify that a method is actually overriding a method in a  
  superclass.  

* **Processing tools:** Annotations can be processed by various tools during  
  compilation or deployment time. These tools can use the information in the  
  annotations to generate code, configuration files, or perform other tasks. For  
  example, a framework might use annotations to configure how a class is mapped  
  to a database table.  

* **Runtime:** Some annotations are available for introspection at runtime using  
  reflection. This allows programs to examine the annotations on classes and  
  methods and act accordingly.  

Here are some key points about Java annotations:

* **They are metadata:** Annotations provide supplemental information about the  
  program, not the core functionality.  
* **Custom vs. predefined:** You can define your own annotations or use  
  predefined annotations that are part of the Java platform or third-party  
  libraries.  
* **Scope:** Annotations can be applied to various program elements like  
  classes, methods, fields, etc.  
* **Retention:** Annotations can have different lifespans. Some are retained  
  only during compilation, while others are available at runtime via reflection.  

Overall, annotations are a powerful tool in Java that can improve code  
readability, maintainability, and enable powerful features provided by  
frameworks and libraries.  


## The @Override annotation


The `@Override` annotation in Java is specifically used for method overriding in  
inheritance. It's a marker annotation introduced in Java 1.5 to improve code  
clarity and catch errors during compilation.  

Here's what `@Override` does:

* **Indicates intent:**  By placing `@Override` before a method declaration in a  
  subclass, you explicitly tell the compiler that you intend to override a  
  method from the superclass.  

* **Compiler checks:** The compiler verifies if the method with the `@Override`  
  annotation actually overrides a method with the same name, parameter list, and  
  return type in the direct superclass. If not, it throws a compilation error.  
  This helps prevent mistakes like typos in method names or accidental overloads  
  (methods with the same name but different parameter lists).  

* **Improved readability:** Using `@Override` makes your code clearer by  
  highlighting methods that are intended to override functionalities from the  
  parent class.

**Things to keep in mind:**

* `@Override` is not mandatory for overriding methods. The compiler can usually  
  figure out if a method is intended to override based on the signature.  
  However, it's considered good practice to use `@Override` for better code  
  clarity and catching potential errors early on.  
* `@Override` is not used for implementing methods in interfaces. Interfaces  
  only declare methods, and subclasses implementing interfaces must provide  
  their own implementation. The compiler inherently checks for this  
  relationship.

Overall, the `@Override` annotation is a simple but effective tool in Java that  
enhances code reliability and maintainability in object-oriented programming.  


```java
package com.zetcode;

class User {

    private final String firstName;
    private final String lastName;
    private final String occupation;

    public User(String firstName, String lastName, String occupation) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.occupation = occupation;
    }

    public String getFirstName() {
        return firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public String getOccupation() {
        return occupation;
    }

    @Override
    public String toString() {
        final StringBuilder sb = new StringBuilder("User{");
        sb.append("firstName='").append(firstName).append('\'');
        sb.append(", lastName='").append(lastName).append('\'');
        sb.append(", occupation='").append(occupation).append('\'');
        sb.append('}');
        return sb.toString();
    }
}


public class Main {

    public static void main(String[] args) {

        User[] users = {
                new User("John", "Doe", "gardener"),
                new User("Roger", "Roe", "driver"),
                new User("Paul", "Smith", "teacher"),
        };

        for (User user : users) {
            System.out.println(user);
        }

    }
}
```

## @SuppressWarnings annotation

The `@SuppressWarnings` annotation in Java is used to instruct the compiler to  
*suppress specific warnings* for the annotated part of the code. This can be  
helpful in situations where you understand the potential issue flagged by the  
compiler but are certain it's not a problem in your specific context.  


* Placed before a class, method, field, parameter, constructor, or local  
  variable.  
* Takes an array of strings as arguments, specifying the warnings to suppress.  
* Common examples of warnings suppressed include:  
    * `unchecked`: Used for raw types (untyped collections) where type safety  
      checks might raise warnings.   
    * `deprecation`: Suppresses warnings about using deprecated methods or
      classes.

* `@SuppressWarnings` is a handy tool for managing compiler warnings, but it  
  should be used thoughtfully and not as a replacement for writing clean and  
  safe code.   


```java
package com.zetcode;

class Being {

    public Being() {

        System.out.println("Being is created");
    }

    public Being(String being) {

        System.out.printf("Being %s is created%n", being);
    }
}

public class Constructor {

    @SuppressWarnings("ResultOfObjectAllocationIgnored")
    public static void main(String[] args) {

        new Being();
        new Being("Tom");
    }
}
```


## @Deprecated annotation


The `@Deprecated` annotation in Java is used to mark classes, methods, fields,  
or constructors that are *no longer recommended for use*. It serves as a  
warning to developers that they should avoid using these elements and consider  
alternatives.  


* *Signaling intent:* By annotating a program element with `@Deprecated`, you  
  indicate that it's discouraged from being used in new code. There might be  
  better alternatives available or the element might be scheduled for removal in  
  future versions.  

* *Compiler warnings:* When the compiler encounters a code element marked as  
  `@Deprecated`, it generates a warning message. This helps developers identify  
  potential issues and encourages them to migrate to the suggested alternatives.  

* *Refactoring:*  The `@Deprecated` annotation is often used during the  
  evolution of APIs. As libraries and frameworks mature, some functionalities  
  might become outdated or replaced by more efficient approaches. Deprecation  
  allows for a gradual transition without breaking existing code that relies on  
  the old elements.  

**Additional features (Java 9 onwards):**

* `since` (optional): Specifies the version in which the element was deprecated.  
  This provides context for developers about the history of the deprecation.  
* `forRemoval` (optional): Indicates that the element is planned for removal in  
  a future major release. This stronger warning encourages developers to find  
  alternatives as soon  as possible.  

The `@Deprecated` annotation is a valuable tool for guiding developers towards  
better practices and maintaining the health of an evolving codebase. It promotes  
code clarity, maintainability, and helps prevent future compatibility issues.  


```java
package com.zetcode;

class PassWordGenerator {

    @Deprecated
    public String generatePassword() {
        return "generated password";
    }

    public String generateSecurePassword() {
        return "a secure password";
    }

}

public class DeprecatedAnnot {

//    @SuppressWarnings("deprecation")
    public static void main(String[] args) {

        var pgen = new PassWordGenerator();
        System.out.println(pgen.generateSecurePassword());
        System.out.println(pgen.generatePassword());

    }
}
```

## Micronaut example

The `Application.java` file:  

```java
package com.example;

import io.micronaut.runtime.Micronaut;

public class Application {

    public static void main(String[] args) {
        Micronaut.run(Application.class, args);
    }
}
```

The `MyController.java` file:  

```java
package com.example.controller;

import io.micronaut.context.annotation.Property;
import io.micronaut.http.HttpStatus;
import io.micronaut.http.MediaType;
import io.micronaut.http.annotation.Body;
import io.micronaut.http.annotation.Controller;
import io.micronaut.http.annotation.Get;
import io.micronaut.http.annotation.Post;
import io.micronaut.http.annotation.Status;

@Controller
public class MyController {

    @Property(name="app.message")
    private String message;

    @Get(uri="/", produces="text/plain")
    public String index() {
        return "Home page";
    }

    @Get(uri="/message", consumes = MediaType.TEXT_PLAIN, produces="text/plain")
    public String message() {
        return message;
    }

    @Post(value = "/echo", consumes = MediaType.TEXT_PLAIN, produces = MediaType.TEXT_PLAIN)
    @Status(HttpStatus.OK)
    public String hello(@Body String text) {
        return text;
//        HttpResponse.ok(text).header(CONTENT_TYPE, MediaType.TEXT_PLAIN)
    }

}
```

The `application.properties` file:  

```java
micronaut.application.name=demo
micronaut.server.port=8000
app.message="hello from Micronaut application"
```

The `client.http` file:  

```
POST http://localhost:8000/echo HTTP/1.1
content-type: text/plain

hi there!

###

GET http://localhost:8000/message
```

