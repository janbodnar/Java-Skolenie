## OOP

There are three widely used programming paradigms:  

- procedural programming
- functional programming
- object-oriented programming

Java is principally an object-oriented programming language. Since Java 8, it  
has support of the functional programming.  

## Object-oriented programming

Object-oriented programming (OOP) is a programming paradigm that uses objects  
and their interactions to design applications and computer programs.  

The following are basic programming concepts in OOP:

- Abstraction
- Polymorphism
- Encapsulation
- Inheritance

The *abstraction* is simplifying complex reality by modeling classes appropriate  
to the problem. It is the process of hiding certain details and showing only  
essential information to the user.  

The *polymorphism* is the ability of an object to take on many forms.

It can be achieved through: 

- method overriding (runtime polymorphism) where a subclass provides a specific  
  implementation of a method that is already provided by one of its  
  superclasses
- method overloading (compile-time polymorphism) where different methods have  
  the same name but different parameters  

The *encapsulation* hides the implementation details of a class from other  
objects.   

The *inheritance* is a way to form new classes using classes that have already
been defined.  

## Objects

Objects are basic building blocks of a Java OOP program. An object is a  
combination of data and methods. In an OOP program, we create objects. These  
objects communicate together through methods. Each object can receive messages,  
send messages, and process data.  

There are two steps in creating an object. First, we define a class. A class is  
a template for an object. It is a blueprint which describes the state and  
behavior that the objects of the class all share. A class can be used to create  
many objects. Objects created at runtime from a class are called instances of  
that particular class.  

```java
package com.zetcode;

class Being {}

public class SimpleObject {

    public static void main(String[] args) {

        Being b = new Being();
        System.out.println(b);
    }
}
```

In our first example, we create a simple object.  

```java
class Being {}
```

This is a simple class definition. The body of the template is empty. It does  
not have any data or methods.  

```java
Being b = new Being();
```

We create a new instance of the `Being` class. For this we have the `new`  
keyword. The `b` variable is the handle to the created object.  
  
```java
System.out.println(b);
```

We print the object to the console to get some basic description of the object.  

When we print an object, we in fact call its `toString` method. But we have not  
defined any method yet. It is because every object created inherits from the  
base Object. It has some elementary functionality which is shared among all  
objects created. One of this is the `toString` method.  


## Object attributes

Object attributes is the data bundled in an instance of a class. The object  
attributes are called instance variables or member fields. An instance variable  
is a variable defined in a class, for which each object in the class has a  
separate copy.  

```java
package com.zetcode;

class Person {

    public String name;
}

public class ObjectAttributes {

    public static void main(String[] args) {

        Person p1 = new Person();
        p1.name = "Jane";

        Person p2 = new Person();
        p2.name = "Beky";

        System.out.println(p1.name);
        System.out.println(p2.name);
    }
}
```

In the above Java code, we have a `Person` class with one member field called  
`name`.  

```java
class Person {

    public String name;
}
```

We declare a name member field. The `public` keyword specifies that the member  
field will be accessible outside the class block.  

```java
Person p1 = new Person();
p1.name = "Jane";
```

We create an instance of the `Person` class and set the name variable to "Jane".  
We use the dot operator to access the attributes of objects.  

```java
Person p2 = new Person();
p2.name = "Beky";
```

We create another instance of the `Person` class. Here we set the variable to  
"Beky".  

```java
System.out.println(p1.name);
System.out.println(p2.name);
```

We print the contents of the variables to the console.  


## Methods

Methods are functions defined inside the body of a class. They are used to  
perform operations with the attributes of our objects. Methods bring modularity  
to our programs.  

Methods are essential in the encapsulation concept of the OOP paradigm. For  
example, we might have a connect method in our AccessDatabase class. We need not  
to be informed how exactly the method connect connects to the database. We only  
have to know that it is used to connect to a database. This is essential in  
dividing responsibilities in programming, especially in large applications.  

Objects group state and behavior. Methods represent the behavioral part of the  
objects.  

```java
package com.zetcode;

class Circle {

    private int radius;

    public void setRadius(int radius) {

        this.radius = radius;
    }

    public double area() {

        return this.radius * this.radius * Math.PI;
    }
}

public class Methods {

    public static void main(String[] args) {

        Circle c = new Circle();
        c.setRadius(5);

        System.out.println(c.area());
    }
}
```

In the code example, we have a `Circle` class. In the class, we define two  
methods. The setRadius method assigns a value to the radius member and the area  
method computes an area of the circle from the class member and a constant.  

```java
private int radius;
```

We have one member field in the class. It is the radius of the circle. The  
private keyword is an access specifier. It tells that the variable is restricted  
to the outside world. If we want to modify this variable from the outside, we  
must use the publicly available `setRadius` method. This way we protect our data.  

```java
public void setRadius(int radius) {

    this.radius = radius;
}
```

This is the `setRadius` method. The this variable is a special variable which we  
use to access the member fields from methods. The `this.radius` is an instance  
variable, while the radius is a local variable, valid only inside the  
`setRadius` method.

```java
Circle c = new Circle();
c.setRadius(5);
```

We create an instance of the `Circle` class and set its radius by calling the  
setRadius method on the object of the circle. The dot operator is used to call  
the method.  

```java
public double area() {

    return this.radius * this.radius * Math.PI;
}
```

The area method returns the area of a circle. The `Math.PI` is a built-in  
constant.  


## Access modifiers

Access modifiers set the visibility of methods and member fields. Java has three  
access modifiers: `public`, `protected`, and `private`. The public members can  
be accessed from anywhere.  

The protected members can be accessed only within the class itself, by inherited  
classes, and other classes from the same package. Finally, the private members  
are limited to the containing type, e.g. only within its class or interface. If  
we do not specify an access modifier, we have a package-private visibility. In  
such a case, members and methods are accessible within the same package.  

Access modifiers protect data against accidental modifications. They make the  
programs more robust.  

Certainly! Here's your data in a markdown table format:

| Class      | Package | Subclass (same package) | Subclass (other package) | World |
|------------|---------|-------------------------|--------------------------|-------|
| `public`   | +       | +                       | +                        | +     |
| `protected`| +       | +                       | +                        | o     |
| `no modifier`| +     | +                       | o                        | o     |
| `private`  | +       | o                       | o                        | o     |


The `+` symbol indicates allowed access, and the `o` symbol indicates restricted access.  

```java
package com.zetcode;

class Person {

    public String name;
    private int age;

    public int getAge() {

        return this.age;
    }

    public void setAge(int age) {

        this.age = age;
    }
}

public class AccessModifiers {

    public static void main(String[] args) {

        Person p = new Person();
        p.name = "Jane";

        p.setAge(17);

        System.out.println(String.format("%s is %d years old",
                p.name, p.getAge()));
    }
}
```

In the above program, we have two member fields: `public` and `private`.

```java
public int getAge() {

    return this.age;
}
```

If a member field is `private`, the only way to access it is via methods. If we  
want to modify an attribute outside the class, the method must be declared  
public. This is an important aspect of data protection.  

```java
public void setAge(int age) {

    this.age = age;
}
```

The `setAge` method enables us to change the private age variable from outside  
of the class definition.  

```java
Person p = new Person();
p.name = "Jane";
```

We create a new instance of the `Person` class. Because the name attribute is  
public, we can access it directly. However, this is not recommended.  

```java
p.setAge(17);
```

The `setAge` method modifies the age member field. It cannot be accessed or  
modified directly, because it is declared private.  

```java
System.out.println(String.format("%s is %d years old",
        p.name, p.getAge()));
```

Finally, we access both members to build a string, which is printed to the  
console.  


The following program shows how access modifiers influence the way members are  
inherited by subclasses.  

```java
package com.zetcode;

class Base {

    public String name = "Base";
    protected int id = 5323;
    private boolean isDefined = true;
}

class Derived extends Base {

    public void info() {

        System.out.println("This is Derived class");
        System.out.println("Members inherited:");
        System.out.println(this.name);
        System.out.println(this.id);
        // System.out.println(this.isDefined);
    }
}

public class ProtectedMember {

    public static void main(String[] args) {

        Derived drv = new Derived();
        drv.info();
    }
}
```

In this program, we have a `Derived` class which inherits from the `Base` class.  
The `Base` class has three member fields, all with different access modifiers.  
The `isDefined` member is not inherited. The `private` modifier prevents this.  

```java
class Derived extends Base {
```

The `Derived` class inherits from the `Base` class. To inherit from another  
class, we use the `extends` keyword.  

```java
System.out.println(this.name);
System.out.println(this.id);
// System.out.println(this.isDefined);
```

The `public` and the `protected` members are inherited by the `Derived` class.  
They can be accessed. The private member is not inherited. The line accessing  
the member field is commented. If we uncommented the line, the code would not  
compile.  


## Constructor

A constructor is a special kind of a method. It is automatically called when the  
object is created. Constructors do not return values and also do not use the  
`void` keyword. The purpose of the constructor is to initiate the state of an  
object. Constructors have the same name as the class. The constructors are  
methods, so they can be overloaded too. Constructors cannot be directly invoked.  

The `new` keyword invokes them. Constructors cannot be declared `synchronized`,  
`final`, `abstract`, `native`, or `static`.  

Constructors cannot be inherited. They are called in the order of inheritance.  
If we do not write any constructor for a class, Java provides an implicit  
default constructor. If we provide any kind of a constructor, then the default  
is not supplied.  

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

public class Main {

    public static void main(String[] args) {

        Being b1 = new Being();
        Being b2 = new Being("Tom");

        System.out.println(b1.getClass());
        System.out.println(b2.getClass());
    }
}
```

We have a `Being` class. This class has two constructors. The first one does not  
take parameters, the second one takes one parameter.  

```java
public Being() {

    System.out.println("Being is created");
}
```

This constructor does not take any parameters.

```java
  public Being(String being) {

      System.out.printf("Being %s is created%n", being);
  }
```

This constructor takes one string parameter.  

```java
new Being();
```

An instance of the Being class is created. The no-argument constructor is called  
upon object creation.

```java
new Being("Tom");
```

Another instance of the `Being` class is created. This time the constructor with  
a parameter is called upon object creation.  


In the next example, we initiate data members of the class. Initiation of  
variables is a typical job for constructors.  

```java
package com.zetcode;

class User {

    private String occupation;
    private String name;

    public User(String name, String occupation) {

        this.name = name;
        this.occupation = occupation;
    }

    public void info() {

        System.out.format("%s is a %s\n", this.name, this.occupation);
    }
}

public class MemberInit {

    public static void main(String[] args) {

        String name = "John Doe";
        String occupation = "gardener";

        User u = new User(name, occupation);
        u.info();
    }
}
```

We have a User class with data members and methods.

```java
private String occupation;
private String name;
```

We have two `private` variables in the class definition.

```java
public User(String name, String occupation) {

    this.name = name;
    this.occupation = occupation;
}
```

In the constructor, we initiate the two data members. The this keyword is a  
handler used to reference the object variables from methods. When the names of  
constructor parameters and the names of members are equal, using this keyword is  
required. Otherwise, the usage is optional.  

```java
User u = new User(name, occupation);
u.info();
```

We create a `MyFriend` object with two arguments. Then we call the `info` method  
of the object.  

## The super keyword

The `super` keyword is a reference variable that is used in subclasses to refer  
to the immediate parent class object.  

It can be use to refer to the parent's:

- instance variable 
- constructor
- method

```java
package com.zetcode;

class Shape {

    int x = 50;
    int y = 50;
}

class Rectangle extends Shape {

    int x = 100;
    int y = 100;

    public void info() {

        System.out.println(x);
        System.out.println(super.x);
    }
}

public class SuperVariable {

    public static void main(String[] args) {

        Rectangle r = new Rectangle();
        r.info();
    }
}
```

In the example, we refer to the parent's variable with the `super` keyword.  

```java
public void info() {

    System.out.println(x);
    System.out.println(super.x);
}
```

Inside the info method, we refer to the parent's instance variable with the
`super.x` syntax.  

If a constructor does not explicitly invoke a superclass constructor, Java  
automatically inserts a call to the no-argument constructor of the superclass.  
If the superclass does not have a no-argument constructor, we get a compile-time  
error.  

```java
package com.zetcode;

class Vehicle {

    public Vehicle() {

        System.out.println("Vehicle created");
    }
}

class Bike extends Vehicle {

    public Bike() {

        // super();
        System.out.println("Bike created");
    }
 }

public class ImplicitSuper {

    public static void main(String[] args) {

        Bike bike = new Bike();
        System.out.println(bike);
    }
}
```

The example demonstrates the implicit call to the parent's constructor.

```java
public Bike() {

    // super();
    System.out.println("Bike created");
}
```

We get the same result if we uncomment the line.


## Multiple constructors

There can be more than one constructor in a class.  

```java
package com.zetcode;

class Vehicle {

    protected double price;

    public Vehicle() {

        System.out.println("Vehicle created");
    }

    public Vehicle(double price) {

        this.price = price;

        System.out.printf("Vehicle created, price %.2f set%n", price);
    }
}

class Bike extends Vehicle {

    public Bike() {

        super();
        System.out.println("Bike created");
    }

    public Bike(double price) {

        super(price);
        System.out.printf("Bike created, its price is: %.2f %n", price);
    }
 }

public class SuperCalls {

    public static void main(String[] args) {

        Bike bike1 = new Bike();
        Bike bike2 = new Bike(45.90);
    }
}
```

The example uses different syntax of super to call different parent  
constructors.  

```java
super();
```

Here, we call the parent's no-argument constructor.

```java
super(price);
```

This syntax calls the parent's constructor that takes one parameter: the bike's
price.

## Constructor chaining

*Constructor chaining* is the ability to call another constructor from a  
constructor. To call another constructor from the same class, we use the this  
keyword. To call another constructor from a parent class, we use the `super`  
keyword.  

```java
package com.zetcode;

class Shape {

    private int x;
    private int y;

    public Shape(int x, int y) {

        this.x = x;
        this.y = y;
    }

    protected int getX() {

        return this.x;
    }

    protected int getY() {

        return this.y;
    }
}

class Circle extends Shape {

    private int r;

    public Circle(int r, int x, int y) {

        super(x, y);
        this.r = r;
    }

    public Circle() {

        this(1, 1, 1);
    }

    @Override
    public String toString() {

        return String.format("Circle: r:%d, x:%d, y:%d", r, getX(), getY());
    }
}

public class ConstructorChaining {

    public static void main(String[] args) {

        Circle c1 = new Circle(5, 10, 10);
        Circle c2 = new Circle();

        System.out.println(c1);
        System.out.println(c2);
    }
}
```

We have a `Circle` class. The class has two constructors. One that takes one  
parameter and one that does not take any parameters.  

```java
class Shape {

    private int x;
    private int y;
...
}
```

The `Shape` class is responsible for dealing with the `x` and `y` coordinates of  
various shapes.  

```java
public Shape(int x, int y) {

    this.x = x;
    this.y = y;
}
```

The constructor of the `Shape` class initiates the x and y coordinates with the  
given parameters.  

```java
protected int getX() {

    return this.x;
}

protected int getY() {

    return this.y;
}
```

We have defined two methods to retrieve the values of the coordinates. The  
members are private, so the only access possible is through methods.  

```java
class Circle extends Shape {

    private int r;
...
}
```

The `Circle` class inherits from the `Shape` class. It defines the `radius`  
member which is specific to this shape.  

```java
public Circle(int r, int x, int y) {

    super(x, y);
    this.r = r;
}
```

The first constructor of the `Circle` class takes three parameters: the  
`radius`, and the `x` and `y` coordinates. With the `super` keyword, we call the  
parent's constructor passing the coordinates. Note that the `super` keyword must  
be the first statement in the constructor. The second statement initiates the  
`radius` member of the `Circle` class.  

```java
public Circle() {

    this(1, 1, 1);
}
```

The second constructor takes no parameters. In such a case, we provide some  
default values. The `this` keyword is used to call the three-parameter constructor  
of the same class, passing three default values. 

```java
@Override
public String toString() {

    return String.format("Circle: r:%d, x:%d, y:%d", r, getX(), getY());
}
```

Inside the `toString` method, we provide a string representation of the `Circle`  
class. To determine the `x` and `y` coordinates, we use the inherited `getX` and  
`getY` methods.  



## Class constants

It is possible to create class constants. These constants do not belong to a  
concrete object. They belong to the class. By convention, constants are written  
in uppercase letters.  

```java
package com.zetcode;

class Math {

    public static final double PI = 3.14159265359;
}

public class ClassConstant {

    public static void main(String[] args) {

        System.out.println(Math.PI);
    }
}
```

We have a `Math` class with a `PI` constant.

```java
public static final double PI = 3.14159265359;
```

The `final` keyword is used to define a constant. The `static` keyword enables  
to refer the member without creating an instance of the class. The `public`  
keyword makes it accessible outside the body of the class.  

## The toString method

Each object has the `toString` method. It returns a human-readable  
representation of an object. The default implementation returns the fully  
qualified name of the type of the Object. When we call the `System.out.println`  
method with an object as a parameter, the `toString` is being called.  

```java
package com.zetcode;

class Being {

    @Override
    public String toString() {

        return "This is Being class";
    }
}

public class ThetoStringMethod {

    public static void main(String[] args) {

        Being b = new Being();
        Object o = new Object();

        System.out.println(o.toString());
        System.out.println(b.toString());
        System.out.println(b);
    }
}
```

We have a Being class in which we override the default implementation of   
the `toString` method.  

```java
@Override
public String toString() {

    return "This is Being class";
}
```

Each class created inherits from the base `Object`. The `toString` method  
belongs to this object class. The `@Override` annotation informs the compiler  
that the element is meant to override an element declared in a superclass. The  
compiler will then check that we did not create any error.  

```java
Being b = new Being();
Object o = new Object();
```

We create two objects: one custom defined and one built-in.

```java
System.out.println(o.toString());
System.out.println(b.toString());
```

We call the `toString` method explicitly on these two objects.

```java
System.out.println(b);
```

As we have specified earlier, placing an object as a parameter to the  
System.out.println will call its `toString` method. This time, we have called  
the method implicitly.  

## Inheritance 

Inheritance is a way to form new classes using classes that have already been  
defined. The newly formed classes are called derived classes, the classes that  
we derive from are called base classes. Important benefits of inheritance are  
code reuse and reduction of complexity of a program. The derived classes  
(descendants) override or extend the functionality of base classes (ancestors).  

```java
package com.zetcode;

class Being {

    public Being() {

        System.out.println("Being is created");
    }
}

class Human extends Being {

    public Human() {

        System.out.println("Human is created");
    }
}

public class Inheritance {

    @SuppressWarnings("ResultOfObjectAllocationIgnored")
    public static void main(String[] args) {

        new Human();
    }
}
```

In this program, we have two classes: a base `Being` class and a derived `Human`  
class. The derived class inherits from the base class.  

```java
class Human extends Being {
```

In Java, we use the extends keyword to create inheritance relations.  

```java
new Human();
```

We instantiate the derived `Human` class.

We can see that both constructors were called. First, the constructor of the  
base class is called, then the constructor of the derived class.  

A more complex example follows.  

```java
package com.zetcode;

class Being {

    static int count = 0;

    public Being() {

        count++;
        System.out.println("Being is created");
    }

    public void getCount() {

        System.out.format("There are %d Beings%n", count);
    }
}

class Human extends Being {

    public Human() {

        System.out.println("Human is created");
    }
}

class Animal extends Being {

    public Animal() {

        System.out.println("Animal is created");
    }
}

class Dog extends Animal {

    public Dog() {

        System.out.println("Dog is created");
    }
}

public class Inheritance2 {

    @SuppressWarnings("ResultOfObjectAllocationIgnored")
    public static void main(String[] args) {

        new Human();
        Dog dog = new Dog();
        dog.getCount();
    }
}
```

With four classes, the inheritance hierarchy is more complicated. The `Human`  
and the `Animal` classes inherit from the Being class and the `Dog` class  
inherits directly from the `Animal` class and indirectly from the `Being` class.  

```java
static int count = 0;
```

We define a static variable. Static members are shared by all instances of a  
class.  

```java
public Being() {

    count++;
    System.out.println("Being is created");
}
```

Each time the `Being` class is instantiated, we increase the count variable by  
one. This way we keep track of the number of instances created.  

```java
class Animal extends Being {
...

class Dog extends Animal {
...
```

The `Animal` inherits from the `Being` and the `Dog` inherits from the `Animal`.  
Indirectly, the `Dog` inherits from the `Being` as well.  

```java
new Human();
Dog dog = new Dog();
dog.getCount();
```

We create instances from the `Human` and from the `Dog` classes. We call the  
getCount method of the `Dog` object.  

## Polymorphism

Polymorphism is the process of using an operator or function in different ways  
for different data input. In practical terms, polymorphism means that if class B  
inherits from class A, it doesn't have to inherit everything about class A; it  
can do some of the things that class A does differently.  

In general, polymorphism is the ability to appear in different forms.  
Technically, it is the ability to redefine methods for derived classes.  
Polymorphism is concerned with the application of specific implementations to an  
interface or a more generic base class.  

Simply put, polymorphism is the ability to redefine methods for derived classes.

```java
package com.zetcode;

abstract class Shape {

    protected int x;
    protected int y;

    public abstract int area();
}

class Rectangle extends Shape {

    public Rectangle(int x, int y) {
        
        this.x = x;
        this.y = y;
    }

    @Override
    public int area() {
        
        return this.x * this.y;
    }
}

class Square extends Shape {

    public Square(int x) {
        
        this.x = x;
    }

    @Override
    public int area() {

        return this.x * this.x;
    }
}

public class Polymorphism {

    public static void main(String[] args) {

        Shape[] shapes = { new Square(5),
            new Rectangle(9, 4), new Square(12) };

        for (Shape shape : shapes) {
            
            System.out.println(shape.area());
        }
    }
}
```

In the above program, we have an abstract `Shape` class. This class morphs into  
two descendant classes: `Rectangle` and `Square`. Both provide their own  
implementation of the area method. Polymorphism brings flexibility and  
scalability to the OOP systems.  

```java
@Override
public int area() {
    
    return this.x * this.y;
}
...
@Override
public int area() {

    return this.x * this.x;
}
```

The `Rectangle` and `Square` classes have their own implementations of the `area`
method.

```java
Shape[] shapes = { new Square(5),
    new Rectangle(9, 4), new Square(12) };
```

We create an array of three shapes.

```java
for (Shape shape : shapes) {
    
    System.out.println(shape.area());
}
```

We go through each shape and call the area method on it. The compiler calls the  
correct method for each shape. This is the essence of polymorphism.  

## Final class, private constructor

A class with a `final` modifier cannot be subclassed. A class with a constructor
that has a `private` modifier cannot be instantiated.

```java
package com.zetcode;

final class MyMath {

    public static final double PI = 3.14159265358979323846;

    // other static members and methods
}


public class FinalClass {

    public static void main(String[] args) {

        System.out.println(MyMath.PI);
    }
}
```

We have a `MyMath` class. This class has some static members and methods. We do  
not want anyone to inherit from our class; therefore, we declare it to be final.  

Furthermore, we also do not want to allow creation of instances from our class.  
We decide it to be used only from a static context. Declaring a private  
constructor, the class cannot be instantiated.  

```java
package com.zetcode;

final class MyMath {

    private MyMath() {}

    public static final double PI = 3.14159265358979323846;

    // other static members and methods
}


public class PrivateConstructor {

    public static void main(String[] args) {

        System.out.println(MyMath.PI);
    }
}
```

Our `MyMath` class cannot be instantiated and cannot be subclassed. This is how  
`java.lang.Math` is designed in Java language.  
