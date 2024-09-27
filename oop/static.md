## static keyword


The `static` keyword is a non-access modifier. The type that has `static`  
modifier does not belong to the instance of a class; it belongs to the class. In  
addition to this, `static` can be used to create class initializers, constants,  
and have imports of `static` variables without class qualification.  

## Usage of static keyword

The static keyword can be applied to:

- variables
- methods
- blocks
- nested classes
- imports

## Java static variable

Static variables are also known as class variables. All instances of a class  
share the same copy of a static variable. They are initialized only once, at the  
start of the execution. A class variable can be accessed directly by the class  
name, without the need to create a instance. One common use of static is to  
create a constant value that is attached to a class.  

## Variable example

```java
package com.zetcode;

import java.util.ArrayList;
import java.util.List;

class Being {
    public static int count = 0; // Initialize count
}

class Cat extends Being {
    public Cat() {
        count++;
    }
}

class Dog extends Being {
    public Dog() {
        count++;
    }
}

class Donkey extends Being {
    public Donkey() {
        count++;
    }
}

public class Main { // Added class declaration
    public static void main(String[] args) { // Corrected main method signature
        List<Being> beings = new ArrayList<>();

        beings.add(new Cat());
        beings.add(new Cat());
        beings.add(new Cat());
        beings.add(new Dog());
        beings.add(new Donkey());

        int nOfBeings = Being.count;

        System.out.format("There are %d beings %n", nOfBeings);
    }
}
```

In the code example, we keep track of beings created with a static variable.  

```java
class Being {

    public static int count;
}
```

A `static` variable is defined. The variable belongs to the `Being` class and is  
shared by all instances of `Being`, including descendants.  

```java
class Cat extends Being {

    public Cat() {
        count++;
    }
}
```

The `Cat` class inherits from Being. It increments the `count` variable.  

```java
class Dog extends Being {

    public Dog() {
        count++;
    }
}
```

The `Dog` class increments the same class variable. So `Dog` and `Cat` refer to  
the same class variable.  

```java
int nOfBeings = Being.count;
```

We get the number of all beings created. We refer to the class variable by its  
class name followed by the dot operator and the variable name.  

## Static variable properties

- static variables have default values.
- static variables can be accessed directly in static and non-static methods.
- static variables are called class variables or static fields.
- static variables are associated with the class, rather than with any object.

```java
class Runner {

    static int x = 11;

    static void fun1() {
        System.out.println(x);
    }

    void fun2() {
        System.out.println(x);
    }
}


public class Main {
    
    public static void main(String[] args) {

        var r = new Runner();

        Runner.fun1();
        r.fun2();
    }
}
```

Common usage:

- Constants: Often used to define constants, such as `public static final int MAX_USERS = 100;`.  
- Counters: Useful for counting instances of a class, like `static int instanceCount;`.  
- Configuration Settings: Store configuration settings that apply to all instances, such as  
  database connection strings.  
- Utility Classes: In utility or helper classes where methods and variables are static, like `Math.PI`.  
- Shared Resources: Manage shared resources, like a static `Logger` instance for logging purposes.  

These uses leverage the class-level scope and memory efficiency of static variables to maintain consistency  
and global access across instances.  


## Static method

Static methods are called without an instance of the object. To call a static  
method, we use the name of the class, the dot operator, and the name of the  
method. Static methods can only work with static variables.  

Static methods are often used to represent data or calculations that do not work with    
object state. For instance, `java.lang.Math` contains static methods for various calculations.   
They are usually shorter methods.  

We use the static keyword to declare a static method. When no static modifier is  
present, the method is said to be an instance method.  

### Static method restrictions

Static method can only call other static methods. They can only access static  
data and cannot refer to `this` and `super`.  

### Static method example

```java
package com.zetcode;

class Basic {

    static int id = 2321;

    public static void showInfo() {

        System.out.println("This is Basic class");
        System.out.format("The Id is: %d%n", id);
    }
}

public class Main {

    public static void main(String[] args) {

        Basic.showInfo();
    }
}
```

In our code example, we define a static `ShowInfo` method.

```java
static int id = 2321;
```

A static method can only work with static variables. Static variables are not  
available to instance methods.  

```java
public static void showInfo() {

    System.out.println("This is Basic class");
    System.out.format("The Id is: %d%n", id);
}
```

This is our static `ShowInfo` method. It works with a static id member.

```java
Basic.showInfo();
```

To invoke a static method, we do not need an object instance. We call the method  
by using the name of the class and the dot operator.  

## The static main method

In Java console and GUI applications, the entry point has the following singnature:

```java
public static void main(String[] args)
```

By declaring the main method static, it can be invoked by the runtime engine  
without having to create an instance of the main class. Since the primary reason  
of main is to bootstrap the application, there is no need to have an instance of  
the main class.  

In addition, if the main method was not static, it would require additional  
contracts such as a default constructor or a requirement of the main class not  
to be abstract. So having a static main method is a less complex solution.  

## Java static block

A code block with the static modifier is called a class initializer. A code  
block without the static modifier is an instance initializer. Class initializers  
are executed in the order they are defined, top down, when the class is loaded.  

A static block executes once in the life cycle of any program, and there is no  
other way to invoke it.  

### Static block example

```java
package com.zetcode;

public class Main {

    private static final int i;

    static {

        System.out.println("Class initializer called");
        i = 6;
    }

    public static void main(String[] args) {

        System.out.println(i);
    }
}
```

This is an example of a static initializer.

```java
static {

    System.out.println("Class initializer called");
    i = 6;
}
```

In the static initializer, we print a message to the console and initialize a  
static variable.  


## Java static import

Static imports allow members (fields and methods) defined in a class as public  
static to be used in Java code without specifying the class in which the field  
is defined.  

### Static import disadvantages

The overuse the static import feature can make our program unreadable and  
unmaintainable, polluting its namespace with all the static members we import.  

### Static import example

```java
package com.zetcode;

import static java.lang.Math.PI;

public class Main {

    public static void main(String[] args) {

        System.out.println(PI);
    }
}
```

In the example, we use the PI constant without its class.

## Java constants

The static modifier, in combination with the final modifier, is also used to  
define constants. The final modifier indicates that the value of this field  
cannot change.  

```java
public static final double PI = 3.14159265358979323846;
```

For example, in `java.lang.Math` we have a constant named `PI`, whose value is  
an approximation of pi (the ratio of the circumference of a circle to its  
diameter).


## Static nested classes

A static nested class is a nested class that can be created without the instance  
of the enclosing class. It has access to the static variables and methods of the  
enclosing class.  

Static nested classes can logically group classes that are only used in one  
place. They increase encapsulation and provide more readable and maintainable  
code.  

### Static nested classes restrictions

Static nested classes cannot invoke non-static methods or access non-static
fields of an instance of the enclosing class.

### Static nested class example

```java
package com.zetcode;

public class Main {

    private static int x = 5;

    static class Nested {

        @Override
        public String toString() {
            return "This is a static nested class; x:" + x;
        }
    }

    public static void main(String[] args) {

        Main.Nested sn = new Main.Nested();
        System.out.println(sn);
    }
}
```

The example presents a static nested class.

```java
private static int x = 5;
```

This is a private static variable of the `JavaStaticNestedClass` class. It can  
be accessed by a static nested class.  

```
static class Nested {

    @Override
    public String toString() {
        return "This is a static nested class; x:" + x;
    }
}
```

A static nested class is defined. It has one method which prints a message and  
refers to the static x variable.  

```java
Main.Nested sn = new Main.Nested();
```

The dot operator is used to refer to the nested class.

## Singleton pattern

Singleton design pattern ensures that one and only one object of a particular  
class is ever constructed during the lifetime of the application.  

```java
public class Singleton {

    private static final Singleton INSTANCE = new Singleton();

    private Singleton() {}

    public static Singleton getInstance() {
        return INSTANCE;
    }
}
```

In this simple code excerpt, we have an internal static reference to the single  
allowed object instance. We access the object via a static method.  
