# Classes

A class is a blueprint from which individual objects are created. A class can  
contain fields (variables) and methods to define the behavior of an object.  

The class definition includes the following:

- Class Name: The name should begin with a capital letter and follow the camel  
  case convention.  
- Class Body: Enclosed in curly braces {}, it contains all the code that  
  provides the behavior of the class including variables, methods, constructors,  
  and more.  
- Access Modifiers: Such as public, private, etc., which determine the  
  visibility of the class.  
- Superclass (if any): The class from which the new class inherits properties  
  and behavior (using extends keyword).  
- Interfaces (if any): The interfaces that the class intends to implement  
  (using implements keyword).  


## Regular class

The `class` keyword is used do define classes, which are templates for creating  
objects. The objects are called instances of a class. A new class is created  
with the `new` keyword.  


Inside a class, we define member fields and member functions. The functions  
defined inside classes are called methods. Member fields and functions are  
accessed through the dot operator.

```java
package com.zetcode;

import java.util.Objects;

class User {

    private String name;
    private String occupation;

    public User(String name, String occupation) {
        this.name = name;
        this.occupation = occupation;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getOccupation() {
        return occupation;
    }

    public void setOccupation(String occupation) {
        this.occupation = occupation;
    }

    @Override
    public String toString() {
        final StringBuilder sb = new StringBuilder("User{");
        sb.append("name='").append(name).append('\'');
        sb.append(", occupation='").append(occupation).append('\'');
        sb.append('}');
        return sb.toString();
    }
}

public class RegularClassEx {

    public static void main(String[] args) {

        var u = new User("John Doe", "gardener");
        System.out.println(u);

        System.out.println(u.getName());
        System.out.println(u.getOccupation());

    }
}
```

In the program, we define the `User` class. The class has two fields: `name` and  
`occupation`. In the class, we also define getter and setter methods for the  
fields and the `toString` method for a string representation of our class.  

```java
class User {
...
}
```

The `class` keyword is used to define a class. Inside the pair of curly brackets  
we define the body of the class.  

```java
private String name;
private String occupation;
```

Two `String` fields are defined.

```java
public User(String name, String occupation) {
    this.name = name;
    this.occupation = occupation;
}
```

This is the constructor of the class; it is a special method that has the same  
name as the class. It is called when an instance of the class is created. In our  
case, we initialize our fields in the constructor.  

```java
public String getName() {
    return name;
}

public void setName(String name) {
    this.name = name;
}

public String getOccupation() {
    return occupation;
}

public void setOccupation(String occupation) {
    this.occupation = occupation;
}
```

For accessing private fields, we have defined two getter and setter methods.  

```java
@Override
public String toString() {
    final StringBuilder sb = new StringBuilder("User{");
    sb.append("name='").append(name).append('\'');
    sb.append(", occupation='").append(occupation).append('\'');
    sb.append('}');
    return sb.toString();
}
```

To get a string representation of an object, we define the `toString` method.  
The method is called when we pass the object to `System.out.println` method.  

```java
var u = new User("John Doe", "gardener");
```

A new instance of the `User` class is created with the `new` keyword. At this  
moment, the constructor of the class is called. We pass the constructor two  
string parameters.  

```java
System.out.println(u);
```

The toString of the class is invoked.

```java
System.out.println(u.getName());
System.out.println(u.getOccupation());
```

On the user object, we call the `getName` and `getOccupation` methods. The  
methods are invoked using the dot operator.  


### Swing Example


```java
package com.zetcode;

import javax.swing.GroupLayout;
import javax.swing.JButton;
import javax.swing.JComponent;
import javax.swing.JFrame;
import java.awt.EventQueue;

public class QuitButtonEx extends JFrame {

    public QuitButtonEx() {

        initUI();
    }

    private void initUI() {

        var quitButton = new JButton("Quit");

        quitButton.addActionListener((event) -> System.exit(0));

        createLayout(quitButton);

        setTitle("Quit button");
        setSize(300, 200);
        setLocationRelativeTo(null);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
    }

    private void createLayout(JComponent... arg) {

        var pane = getContentPane();
        var gl = new GroupLayout(pane);
        pane.setLayout(gl);

        gl.setAutoCreateContainerGaps(true);

        gl.setHorizontalGroup(gl.createSequentialGroup()
                .addComponent(arg[0])
        );

        gl.setVerticalGroup(gl.createSequentialGroup()
                .addComponent(arg[0])
        );
    }

    public static void main(String[] args) {

        EventQueue.invokeLater(() -> {
            
            var ex = new QuitButtonEx();
            ex.setVisible(true);
        });
    }
}
```


## Abstract class

An abstract class in an unfinished class. It must be implemented in its  
subclasses. Abstract class is created with the abstract keywords. We can create  
abstract methods and member fields.  


The purpose of an abstract class is to provide a common definition for  
descendant classes.  

Abstract classes cannot be instantiated. If a class contains at least one  
abstract method, it must be declared abstract too. Abstract methods cannot be  
implemented; they merely declare the methods' signatures.  

```java
package com.zetcode;

abstract class Drawing {

    protected int x = 0;
    protected int y = 0;

    public abstract double area();

    public String getCoordinates() {

        return String.format("x: %d, y: %d", this.x, this.y);
    }
}

class Circle extends Drawing {

    private int r;

    public Circle(int x, int y, int r) {

        this.x = x;
        this.y = y;
        this.r = r;
    }

    @Override
    public double area() {

        return this.r * this.r * Math.PI;
    }

    @Override
    public String toString() {

        return String.format("Circle at x: %d, y: %d, radius: %d",
                this.x, this.y, this.r);
    }
}

public class AbstractClassEx {

    public static void main(String[] args) {

        Circle c = new Circle(12, 45, 22);

        System.out.println(c);
        System.out.format("Area of circle: %f%n", c.area());
        System.out.println(c.getCoordinates());
    }
}
```

We have an abstract base `Drawing` class. The class defines two member fields,  
defines one method and declares one method. One of the methods is abstract, the  
other one is fully implemented. The `Drawing` class is abstract because we cannot  
draw it. We can draw a circle, a dot, or a square, but we cannot draw a  
"drawing". The `Drawing` class has some common functionality to the objects that  
we can draw.  

```java
abstract class Drawing {
```

We use the `abstract` keyword to define an abstract class.

```java
public abstract double area();
```

An abstract method is also preceded with a `abstract` keyword. A `Drawing` class  
is an idea. It is unreal and we cannot implement the area method for it. This is  
the kind of situation where we use abstract methods. The method will be  
implemented in a more concrete entity like a circle.  

```java
class Circle extends Drawing {
```

A `Circle` is a subclass of the Drawing class. Therefore, it must implement the  
abstract `area` method.

```java
@Override
public double area() {

    return this.r * this.r * Math.PI;
}
```

Here we are implementing the area method.


## Nested class

It is possible to define a class within another class. Such class is called a  
nested class in Java terminology. A class that is not a nested class is called a  
top-level class.  

Java has four types of nested classes:

- Static nested classes
- Inner classes
- Local classes
- Anonymous classes

Using nested classes may increase the readability of the code and improve the  
organization of the code. Inner classes are often used as callbacks in GUI. For  
example in Java Swing toolkit.  


## Static nested class

A static nested class is a nested class that can be created without the instance  
of the enclosing class. It has access to the static variables and methods of the  
enclosing class.  

Static nested classes are used when you want to logically group classes that are  
only used in one place  

Usage: 

- To associate a class with its outer class: When a class is useful to only one  
  other class, it makes sense to keep it nested and private to the outer class.  
- For enum-like structures: When you need a set of predefined constants or types  
  that are closely related to an outer class.  
- In Builder patterns: Often used in creating complex objects with multiple  
  parameters, where the Builder would be a static nested class.  
- For Iterator implementations: When creating custom iterators for a collection  
  class.  
- In Constant utility classes: To group related constants used by the outer  
  class, making them static allows for easy access without instantiation.  

```java
package com.zetcode;

public class SNCTest {

    private static int x = 5;

    static class Nested {

        @Override
        public String toString() {
            return "This is a static nested class; x:" + x;
        }
    }

    public static void main(String[] args) {

        SNCTest.Nested sn = new SNCTest.Nested();
        System.out.println(sn);
    }
}
```

The example presents a static nested class.

```java
private static int x = 5;
```

This is a private static variable of the `SNCTest` class. It can be accessed by  
a static nested class.  

```java
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
SNCTest.Nested sn = new SNCTest.Nested();
```

The dot operator is used to refer to the nested class.  

### Builder pattern

Builder pattern with a static nested class.  

```java
package com.zetcode;

public class NutritionalFacts {
    private final int sodium;
    private final int fat;
    private final int carbo;

    public int getSodium(){
        return sodium;
    }

    public int getFat(){
        return fat;
    }

    public int getCarbo(){
        return carbo;
    }

    public static class Builder {
        private int sodium;
        private int fat;
        private int carbo;

        public Builder sodium(int s) {
            this.sodium = s;
            return this;
        }

        public Builder fat(int f) {
            this.fat = f;
            return this;
        }

        public Builder carbo(int c) {
            this.carbo = c;
            return this;
        }

        public NutritionalFacts build() {
            return new NutritionalFacts(this);
        }
    }

    @Override
    public String toString() {
        final StringBuilder sb = new StringBuilder("NutritionalFacts{");
        sb.append("sodium=").append(sodium);
        sb.append(", fat=").append(fat);
        sb.append(", carbo=").append(carbo);
        sb.append('}');
        return sb.toString();
    }

    private NutritionalFacts(Builder b) {
        this.sodium = b.sodium;
        this.fat = b.fat;
        this.carbo = b.carbo;
    }
}
```

---

```java
package com.zetcode;

public class Main {

    public static void main(String[] args) {

        NutritionalFacts nfacts = new NutritionalFacts.Builder()
                .sodium(10)
                .carbo(15)
                .fat(5).build();

        System.out.println(nfacts);
    }

}
```

### Constant utility class

Constant utility class as nested static class.  

```java
public class Main {

    class Constants {

        // Static nested class
        public static class Database {
            public static final String URL = "jdbc:mysql://localhost:3306/myDatabase";
            public static final String USER = "username";
            public static final String PASSWORD = "password";
            // Other database constants...
        }

        // Another static nested class
        public static class Configuration {
            public static final String FILE_PATH = "/path/to/config/";
            // Other configuration constants...
        }
    }

    public static void main(String[] args) {
        // Accessing constants from the static nested classes
        String dbUrl = Constants.Database.URL;
        String configPath = Constants.Configuration.FILE_PATH;

        System.out.println(dbUrl);
        System.out.println(configPath);
    }
}
```


## Inner class

An instance of a normal or top-level class can exist on its own. By contrast, an  
instance of an inner class cannot be instantiated without being bound to a  
top-level class. Inner classes are also called member classes. They belong to  
the instance of the enclosing class. Inner classes have access to the members of  
the enclosing class.  

```java
package com.zetcode;

public class InnerClassTest {

    private int x = 5;

    class Inner {

        @Override
        public String toString() {
            return "This is Inner class; x:" + x;
        }
    }

    public static void main(String[] args) {

        InnerClassTest nc = new InnerClassTest();
        InnerClassTest.Inner inner = nc.new Inner();

        System.out.println(inner);
    }
}
```

A nested class is defined in the `InnerClassTest` class. It has access to the  
member `x` variable.

```java
class Inner {

    @Override
    public String toString() {
        return "This is Inner class; x:" + x;
    }
}
```

An Inner class is defined in the body of the `InnerClassTest` class.  

```java
InnerClassTest nc = new InnerClassTest();
```

First, we need to create an instance of the top-level class. Inner classes  
cannot exist without an instance of the enclosing class.  

```java
InnerClassTest.Inner inner = nc.new Inner();
```

Once we have the top-level class instantiated, we can create the instance of the  
inner class.  


### Inner member class


In this example, `Engine` is a *Member Inner Class* of `Car`. It makes sense to  
encapsulate Engine within `Car` because an engine is an integral part of a car,  
and it's not intended to be used independently. The `start` method of `Engine`  
can access the model field of the outer `Car` class, demonstrating the close  
relationship between the two classes.  

```java
package com.zetcode;

class Car {
    private final String model;
    private final Engine engine;

    public Car(String model) {
        this.model = model;
        this.engine = new Engine();
    }

    public void startEngine() {
        engine.start();
    }

    // Member inner class
    private class Engine {
        public void start() {
            System.out.println(model + " engine started.");
        }
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        Car car = new Car("Tesla Model S");
        car.startEngine(); // Outputs: Tesla Model S engine started.
    }
}
```


### Swing example 

A close listenter is implemented as an inner class.  

```java
package com.zetcode;

import javax.swing.GroupLayout;
import javax.swing.JButton;
import javax.swing.JComponent;
import javax.swing.JFrame;
import java.awt.EventQueue;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class InnerClassEx extends JFrame {

    public InnerClassEx() {

        initUI();
    }

    private void initUI() {

        var closeBtn = new JButton("Close");

        var listener = new ButtonCloseListener();
        closeBtn.addActionListener(listener);

        createLayout(closeBtn);

        setTitle("Inner class example");
        setLocationRelativeTo(null);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
    }

    private void createLayout(JComponent... arg) {

        var pane = getContentPane();
        var gl = new GroupLayout(pane);
        pane.setLayout(gl);

        gl.setAutoCreateContainerGaps(true);
        gl.setAutoCreateGaps(true);

        gl.setHorizontalGroup(gl.createSequentialGroup()
                .addComponent(arg[0])
                .addGap(220)
        );

        gl.setVerticalGroup(gl.createParallelGroup()
                .addComponent(arg[0])
                .addGap(220)
        );

        pack();
    }

    private class ButtonCloseListener implements ActionListener {

        @Override
        public void actionPerformed(ActionEvent e) {
            System.exit(0);
        }
    }

    public static void main(String[] args) {

        EventQueue.invokeLater(() -> {
            
            var ex = new InnerClassEx();
            ex.setVisible(true);
        });
    }
}
```



## Local class

A local class in Java is defined within a block, typically within a method. They  
are used to encapsulate complex behavior that is needed only in a specific  
method, thereby keeping the logic local to where it is used.  

A local class is a special case of an inner class. Local classes are classes  
that are defined in a block. (A block is a group of zero or more statements  
between braces.) A local class has access to the members of its enclosing class.  

In addition, a local class has access to local variables if they are declared  
final. The reason for this is technical. The lifetime of an instance of a local  
class can be much longer than the execution of the method in which the class is  
defined. To solve this, the local variables are copied into the local class. To  
ensure that they are later not changed, they have to be declared final.  

Local classes cannot be `public`, `private`, `protected`, or `static`. They are  
not allowed for local variable declarations or local class declarations. Except  
for constants that are declared `static` and `final`, local classes cannot  
contain `static` fields, methods, or classes.   

```java
package com.zetcode;

public class LocalClassEx {

    public static void main(String[] args) {

        final int x = 5;

        class Local {

            @Override
            public String toString() {
                return "This is Local class; x:" + x;
            }
        }

        Local loc = new Local();
        System.out.println(loc);
    }
}
```

A local class is defined in the body of the main method.

```java
@Override
public String toString() {
    return "This is Local class; x:" + x;
}
```

A local class can access local variables if they are declared final.  


A local `Operation` class used to perform operations inside a  
`calculateOperation` method.  

```java
package com.zetcode;

class Calculator {

    private int x;
    private int y;

    public Calculator(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public void calculateOperation(String operation) {
        // Local class inside a method
        class Operation {
            void perform() {
                if ("add".equals(operation)) {
                    int res = x + y;
                    System.out.println(res);
                } else if ("sub".equals(operation)) {
                    int res = x - y;
                    System.out.println(res);
                }
            }
        }

        Operation op = new Operation();
        op.perform();
    }
}

public class Main {
    public static void main(String[] args) {
        var calc = new Calculator(10, 5);
        calc.calculateOperation("add");
        calc.calculateOperation("sub");
    }
}
```

## Anonymous class

Anonymous classes are local classes that do not have a name. They enable us to  
declare and instantiate a class at the same time. We can use anonymous classes  
if we want to use the class only once. An anonymous class is defined and  
instantiated in a single expression. Anonymous inner classes are also used where  
the event handling code is only used by one component and therefore does not  
need a named reference.  

An anonymous class must implement an interface or inherit from a class. But the  
implements and extends keywords are not used. If the name following the new  
keyword is the name of a class, the anonymous class is a subclass of the named  
class. If the name following new specifies an interface, the anonymous class  
implements that interface and extends the `Object`.  

Since an anonymous class has no name, it is not possible to define a constructor  
for an anonymous class. Inside the body of an anonymous class we cannot define  
any statements; only methods or members.  

Anonymous classes are particularly useful in scenarios where: 

- We need to implement an interface with only one or two methods, like event  
  listeners/handlers in GUI applications.  
- We want to override the behavior of a method of a superclass for a one-time  
  use without creating a separate subclass.  
- We writing quick-and-dirty code to test out a concept and don't want to  
  clutter your codebase with named classes.  

### Declare & instantiate

In Java, when we create an anonymous class, we actually declare and  
instantiate it at the same time. The 'extends' keyword is not used explicitly.  
Instead, we write the superclass or interface name followed by a pair of curly  
braces. Inside these braces, we provide the implementation details of our  
anonymous class.  

```java
Animal myAnimal = new Animal() {
    @Override
    public void eat() {
        System.out.println("This animal eats anonymously.");
    }
};
```

In this example, `new Animal()` implies that the anonymous class is extending  
the `Animal` class, and within the curly braces `{}`, we override the `eat`  
method.  

### Extending a class 

```java
package  com.zetcode;

class Animal {
    void eat() {
        System.out.println("Animal is eating.");
    }
}

public class Main {

    public static void main(String[] args) {
        
        Animal myAnimal = new Animal() {
            void eat() {
                System.out.println("Anonymous Animal is eating.");
            }
        };

        myAnimal.eat(); 
    }
}
```

### Implementing an interface

```java
package com.zetcode;

public class AnonymousClass {

   interface Message {
        public void send();
    }

    public void createMessage() {

        Message msg = new Message() {

            @Override
            public void send() {
                System.out.println("This is a message");
            }
        };

        msg.send();
    }

    public static void main(String[] args) {

        AnonymousClass ac = new AnonymousClass();
        ac.createMessage();
    }
}
```

In this code example, we create an anonymous class.

```java
interface Message {
    public void send();
}
```

An anonymous class must be either a subclass or must implement an interface. Our  
anonymous class will implement a `Message` interface. Otherwise, the type would  
not be recognized by the compiler.  

```java
public void createMessage() {

    Message msg = new Message() {

        @Override
        public void send() {
            System.out.println("This is a message");
        }
    };

    msg.send();
}
```

An anonymous class is a local class, hence it is defined in the body of a  
method. An anonymous class is defined in an expression; therefore, the enclosing  
right bracket is followed by a semicolon.  

### Swing example

```java
package com.zetcode;

import javax.swing.GroupLayout;
import javax.swing.JButton;
import javax.swing.JComponent;
import javax.swing.JFrame;
import java.awt.EventQueue;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class AnonymousInnerClass extends JFrame {

    public AnonymousInnerClass() {

        initUI();
    }

    private void initUI() {

        var closeBtn = new JButton("Close");

        closeBtn.addActionListener(new ActionListener() {

            @Override
            public void actionPerformed(ActionEvent event) {
                System.exit(0);
            }
        });

        createLayout(closeBtn);

        setTitle("Anonymous inner class");
        setLocationRelativeTo(null);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
    }

    private void createLayout(JComponent... arg) {

        var pane = getContentPane();
        var gl = new GroupLayout(pane);
        pane.setLayout(gl);

        gl.setAutoCreateContainerGaps(true);
        gl.setAutoCreateGaps(true);

        gl.setHorizontalGroup(gl.createSequentialGroup()
                .addComponent(arg[0])
                .addGap(220)
        );

        gl.setVerticalGroup(gl.createParallelGroup()
                .addComponent(arg[0])
                .addGap(220)
        );

        pack();
    }

    public static void main(String[] args) {

        EventQueue.invokeLater(() -> {

            var ex = new AnonymousInnerClass();
            ex.setVisible(true);
        });
    }
}
```
