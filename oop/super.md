
## The super keyword


The `super` keyword in Java is used to refer to the parent class's members  
(fields, methods, constructors).  

Here are its primary uses:

1. Calling Parent Class Constructor:
   - To explicitly call a specific constructor of the parent class, use  
     `super(arguments)`.
   - This must be the first statement in the child class's constructor.  
   - If you don't explicitly call a parent constructor, the default no-argument  
     constructor is called implicitly.

2. Accessing Parent Class Members:
   - To access a parent class's field or method that is hidden by a child  
     class's member with the same name, use `super.fieldName` or  
     `super.methodName()`.  


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

## Key points

- `super` always refers to the immediate parent class.
- You can use `super` to access both fields and methods.
- When calling a parent class constructor, it must be the first statement  
  in the child class's constructor.
  
