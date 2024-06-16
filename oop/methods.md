# Methods

In object oriented programming, we work with objects. Objects are basic building  
blocks of a program. Objects consists of data and methods. Methods change the  
state of the objects created. They are the dynamic part of the objects; the data  
is the static part.  

A *method* is a code block containing a series of statements. Methods must be  
declared within a class. It is a good programming practice that methods do only  
one specific task. Methods bring modularity to programs. Proper use of methods  
brings the following advantages:  

- Reducing duplication of code
- Decomposing complex problems into simpler pieces
- Improving clarity of the code
- Reuse of code
- Information hiding
- Java method characteristics

Basic characteristics of methods are:  

- Access level
- Return value type
- Method name
- Method parameters
- Parentheses
- Block of statements
 
Access level of methods is controlled with access modifiers. They set the  
visibility of methods. They determine who can call the method. Methods may  
return a value to the caller. If our method returns a value, we declare its data  
type. If not, we use the void keyword to indicate that our method does not  
return any value.  

Method parameters are surrounded by parentheses and separated by commas. Empty  
parentheses indicate that the method requires no parameters. The method block is  
surrounded with {} characters. The block contains one or more statements that  
are executed when the method is invoked. It is legal to have an empty method  
block.  

## Method signature

A method signature is a unique identification of a method for the Java compiler.  
The signature consists of a method name, and the type and kind (value,  
reference, or output) of each of its formal parameters. Method signature does  
not include the return type.  

## Method names

Method names can be composed of any combination of letters, numbers, underscores  
(_), and dollar signs ($), but they must not begin with a number. Additionally,  
method names are case-sensitive and should follow the `camelCase` convention for  
readability.   

The method names are verbs or verbs followed by adjectives or nouns. Each  
subsequent word starts with an uppercase character. The following are typical  
names of methods in Java:    

- execute
- findId
- setName
- getName
- checkIfValid
- testValidity


## Simple example

```java
package com.zetcode;

class Base {

    public void showInfo() {

        System.out.println("This is Base class");
    }
}

public class ShowInfoMethod {

    public static void main(String[] args) {

        Base bs = new Base();
        bs.showInfo();
    }
}
```

We have a `showInfo` method that prints the name of its class.  

```java
class Base {

    public void showInfo() {

        System.out.println("This is Base class");
    }
}
```

Each method must be defined inside a class. It must have a name. In our case,  
the name is showInfo. The keywords that precede the name of the method are   
access specifier and the return type. Parentheses follow the name of the method.  
They may contain parameters of the method. Our method does not take any  
parameters.  

```java
public static void main(String[] args) {
...
}
```

This is the main method. It is the entry point to each console or GUI Java  
application. The method takes a string array of arguments.  

```java
Base bs = new Base();
bs.showInfo();
```

We create an instance of the Base class. We call the showInfo method upon the  
object. We say that the method is an instance method because it needs an  
instance to be called. The method is called by specifying the object instance,  
followed by the member access operator — the dot, followed by the method name.  

## Method parameters

A parameter is a value passed to the method. Methods can take one or more  
parameters. If methods work with data, we must pass the data to the methods.  
This is done by specifying them inside the parentheses. In the method  
definition, we must provide a name and type for each parameter.  

```java
package com.zetcode;

class AddValues {

    public int addTwoValues(int x, int y) {

        return x + y;
    }

    public int addThreeValues(int x, int y, int z) {

        return x + y + z;
    }
}

public class Addition {

    public static void main(String[] args) {

        AddValues a = new AddValues();
        int x = a.addTwoValues(12, 13);
        int y = a.addThreeValues(12, 13, 14);

        System.out.println(x);
        System.out.println(y);
    }
}
```

In the above example, we have an `AddValues` class which has two methods. One of  
them takes two parameters, the other one takes three parameters.  

```java
public int addTwoValues(int x, int y) {

    return x + y;
}
```

The `addTwoValues` method takes two parameters. These parameters have int type.  
The method also returns an integer to the caller. We use the return keyword to  
return a value from the method.  

```java
public int addThreeValues(int x, int y, int z) {

    return x + y + z;
}
```

The `addThreeValues` is similar to the previous method, but it takes three  
parameters.

```java
int x = a.addTwoValues(12, 13);
```

We call the `addTwoValues` method of the `AddValues` object. It takes two  
values. These values are passed to the method. The method returns a value which  
is assigned to the x variable.  


## Variable number of arguments

A method can take variable number of arguments. For this we use ellipsis.  


```java
package com.zetcode;

public class SumOfValues {

    public static int sum(int...vals) {

        int sum = 0;

        for (int val : vals) {
            sum += val;
        }

        return sum;
    }

    public static void main(String[] args) {

        int s1 = sum(1, 2, 3);
        int s2 = sum(1, 2, 3, 4, 5);
        int s3 = sum(1, 2, 3, 4, 5, 6, 7);

        System.out.println(s1);
        System.out.println(s2);
        System.out.println(s3);
    }
}
```

We create a sum method which can take variable number of arguments. The method  
calculates the sum of integers passed to the method.  

```java
int s1 = sum(1, 2, 3);
int s2 = sum(1, 2, 3, 4, 5);
int s3 = sum(1, 2, 3, 4, 5, 6, 7);
```

We call the sum method three times. In each case, we pass different number of  
parameters to the method.

```java
public static int sum(int...vals) {
...
}
```

The `sum` method can take variable number of integer values. All values are  
added to an array.  

```java
int sum = 0;

for (int val : vals) {
    sum += val;
}

return sum;
```

We compute the sum of the values and return the calculated sum.  


## Passing arguments by value

In Java, arguments are always passed by value to methods. When we pass primitive  
types, the copies of the values are sent to the methods. In case of objects,  
copies of the references are handed to the methods.  

Java does not support passing arguments by reference, like C# or C++.  

```java
package com.zetcode;

class Cat {}
class Dog {}

public class PassByValue {

    private static void tryChangeInteger(int x) {

        x = 15;
    }

    private static void tryChangeObject(Object o) {

        Dog d = new Dog();
        o = d;
    }

    public static void main(String[] args) {

        int n = 10;
        tryChangeInteger(n);
        System.out.println(n);

        Cat c = new Cat();
        tryChangeObject(c);
        System.out.println(c.getClass());
    }
}
```

The example shows that it is not possible to change the values of primitive  
types and the references to objects inside methods.  

```java
private static void tryChangeInteger(int x) {

    x = 15;
}
```

The value of the passed variable is copied to the local variable `x`. Assigning  
a new value to the `x` variable does not affect the outside variable.  

```java
private static void tryChangeObject(Object o) {

    Dog d = new Dog();
    o = d;
}
```

The same applies for objects. We are passing copies of references to methods.  
The o is a local variable that refers to the `Dog` object. The object defined  
outside the `tryChangeObject` is not affected.  

```java
int n = 10;
tryChangeInteger(n);
System.out.println(n);
```

We define the `n` variable and pass it to the `tryChangeInteger` method. Later,  
we print it to check if it was modified.  

```java
Cat c = new Cat();
tryChangeObject(c);
System.out.println(c.getClass());
```

We define a `Cat` object and pass it to the `tryChangeObject` method.  

```
$ java com.zetcode.PassByValue
10
class com.zetcode.Cat
```

From the output we can see that neither the primitive value nor the object were  
modified.  

## Method overloading

Method overloading allows the creation of several methods with the same name  
which differ in the type of the input.  

What is method overloading good for? Qt library gives a nice example for the  
usage. The QPainter class has three methods to draw a rectangle. Their name is  
drawRect and their parameters differ. One takes a reference to a floating point  
rectangle object, another takes a reference to an integer rectangle object, and  
the last one takes four parameters: `x`, `y`, `width`, and `height`.  

If the C++ language, which is the language in which Qt is developed, didn't have  
method overloading, the creators of the library would have to name the methods  
like drawRectRectF, drawRectRect, drawRectXYWH. The solution with method  
overloading is more elegant.  

```java
package com.zetcode;

class Sum {

    public int getSum() {

        return 0;
    }

    public int getSum(int x) {

        return x;
    }

    public int getSum(int x, int y) {

        return x + y;
    }
}

public class Overloading {

    public static void main(String[] args) {

        Sum s = new Sum();
        System.out.println(s.getSum());
        System.out.println(s.getSum(5));
        System.out.println(s.getSum(5, 10));
    }
}
```

We have three methods called `setSum`. They differ in input parameters.  


### Swing example

```java
package com.zetcode;

import java.awt.Color;
import java.awt.EventQueue;
import java.awt.Graphics;
import java.awt.Graphics2D;
import java.awt.Polygon;
import javax.swing.JFrame;
import javax.swing.JPanel;

class DrawPanel extends JPanel {

    private void doDrawing(Graphics g) {

        var g2d = (Graphics2D) g;

        g2d.setColor(new Color(125, 167, 116));

        int[] xPoints = {5, 50, 90, 60};
        int[] yPoints = {20, 5, 75, 150};
        int nPoints = xPoints.length;

        // Use the first overloaded method
        g2d.fillPolygon(xPoints, yPoints, nPoints);

        g2d.setColor(new Color(42, 179, 231));

        Polygon polygon = new Polygon(new int[]{100, 170, 110, 195},
                new int[]{120, 150, 180, 215}, 4);

        // Use the second overloaded method
        g2d.fillPolygon(polygon);
      }

    @Override
    public void paintComponent(Graphics g) {

        super.paintComponent(g);
        doDrawing(g);
    }
}

public class PolygonsEx extends JFrame {

    public PolygonsEx() {

        initUI();
    }

    private void initUI() {

        var drawPanel = new DrawPanel();
        add(drawPanel);

        setSize(360, 300);
        setTitle("Polygons");
        setLocationRelativeTo(null);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {

        EventQueue.invokeLater(() -> {

            var ex = new PolygonsEx();
            ex.setVisible(true);
        });
    }
}
```

## Recursion

Recursion, in mathematics and computer science, is a way of defining methods in  
which the method being defined is applied within its own definition. In other  
words, a recursive method calls itself to do its job. Recursion is a widely used  
approach to solve many programming tasks. Every problem solved using a recursion  
can be worked out with the iteration too.  

A typical example is the calculation of a factorial.  

```java
package com.zetcode;

public class Recursion {

    static int factorial(int n) {

        if (n == 0) {

            return 1;
        } else {

            return n * factorial(n - 1);
        }
    }

    public static void main(String[] args) {

        System.out.println(factorial(6));
        System.out.println(factorial(15));
    }
}
```

In this code example, we calculate the factorial of two numbers.

```java
return n * factorial(n - 1);
```

Inside the body of the factorial method, we call the factorial method with a  
modified argument. The function calls itself. This is the essence of the  
recursion algorithm.  

## Method scope

A variable declared inside a method has a method scope. The scope of a name is  
the region of program within which it is possible to refer to the entity  
declared by the name without the qualification of the name. A variable which is  
declared inside a method has a method scope. It is also called a local scope.  
The variable is valid only in this particular method.  

```java
package com.zetcode;

class Test {

    int x = 1;

    public void exec1() {

        System.out.println(this.x);
        System.out.println(x);
    }

    public void exec2() {

        int z = 5;

        System.out.println(x);
        System.out.println(z);
    }
}

public class MethodScope {

    public static void main(String[] args) {

        Test ts = new Test();
        ts.exec1();
        ts.exec2();
    }
}
```

In this example, we have the `x` variable defined outside the instance methods.  
The variable has a class scope. It is valid everywhere inside the definition of  
the Test class, e.g. between its curly brackets.  

```java
public void exec1() {

    System.out.println(this.x);
    System.out.println(x);
}
```

The `x` variable, also called the `x `field, is an instance variable. It is  
accessible through `this` keyword. It is also valid inside the `exec1` method  
and can be referred by its bare name. Both statements refer to the same  
variable.

```java
public void exec2() {

    int z = 5;

    System.out.println(x);
    System.out.println(z);
}
```

The `x` variable can be accessed also in the `exec2` method. The `z` variable is  
defined in the `exec2` method. It has a method scope. It is valid only in this  
method.  

A variable defined inside a method has a local/method scope. If a local variable  
has the same name as an instance variable, it shadows the instance variable. The  
instance variable is still accessible inside the method with this.  

```java
package com.zetcode;

class Test {

    int x = 1;

    public void exec() {

        int x = 3;

        System.out.println(this.x);
        System.out.println(x);
    }
}

public class Shadowing {

    public static void main(String[] args) {

        Test t = new Test();
        t.exec();
    }
}
```

We declare an instance variable `x`. We declare another `x` variable inside the  
`exec` method. Both variables have the same name, but they are not in conflict  
because they reside in different scopes.  

```java
System.out.println(this.x);
System.out.println(x);
```

The variables are accessed differently. The `x` variable defined inside the  
method, also called a local variable `x`, is simply accessed by its name. The  
instance variable can be referred by using with `this`.  


## Static methods

Static methods are called without an instance of the object. To call a static  
method, we use the name of the class and the dot operator. Static methods can  
only work with static variables. Static methods are often used to represent data  
or calculations that do not change in response to object state. An example is a  
math library which contains static methods for various calculations.  

We use the static keyword to declare a static method or a static variable. When  
no static modifier is present, the method is said to be an instance method. We  
cannot use this keyword in static methods; it can be used in instance methods  
only.  

```java
package com.zetcode;

class Basic {

    static int id = 2321;

    public static void showInfo() {

        System.out.println("This is Basic class");
        System.out.format("The Id is: %d%n", id);
    }
}

public class StaticMethod {

    public static void main(String[] args) {

        Basic.showInfo();
    }
}
```

In our code example, we define a static `ShowInfo` method.  

```
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

## Hiding methods

In case of static methods, a method in the derived class with the same signature  
as in the base class hides the one in the base class. The method to be called is  
determined at compile time. This process is referred to as early or static  
binding.  

```java
package com.zetcode;

class Base {

    public static void showInfo() {

        System.out.println("This is Base class");
    }
}

class Derived extends Base {

    public static void showInfo() {

        System.out.println("This is Derived class");
    }
}

public class Hiding {

    public static void main(String[] args) {

        Base.showInfo();
        Derived.showInfo();
    }
}
```

We have two classes: `Derived` and `Base`. The `Derived` class inherits from the  
`Base` class. Both have a method called `showInfo`.  

```
class Derived extends Base {

    public static void showInfo() {

        System.out.println("This is Derived class");
    }
}
```

The static class method `showInfo` of the `Derived` class hides the `showInfo`  
method of the `Base` class.  

```java
Base.showInfo();
Derived.showInfo();
```

We call the `showInfo` method for both classes. Each class calls its own method.  

## Overriding methods

Overriding happens when we create an instance method of a derived class with the  
same signature and return type as an instance method in the base class. The  
method to be executed is determined at runtime. The determining of the method to  
be executed at runtime is called late or dynamic binding.  

We might want to use the `@Override` annotation that instructs the compiler that  
we intend to override a method in the superclass. It helps prevent some  
programming errors.  

```java
package com.zetcode;

class Base {

    public void showInfo() {

        System.out.println("This is Base class");
    }
}

class Derived extends Base {

    @Override
    public void showInfo() {

        System.out.println("This is Derived class");
    }
}

public class Overriding {

    public static void main(String[] args) {

        Base[] objs = { new Base(), new Derived(), new Base(),
            new Base(), new Base(), new Derived() };

        for (Base obj : objs) {

            obj.showInfo();
        }
    }
}
```

We create an array of the `Base` and `Derived` objects. We go through the array  
and invoke the `showInfo` method upon all of them.  

```java
@Override
public void showInfo() {

    System.out.println("This is Derived class");
}
```

Here we are overriding the `showInfo` method of the `Base` class.

```java
Base[] objs = { new Base(), new Derived(), new Base(),
    new Base(), new Base(), new Derived() };
```
 
Here we create an array of `Base` and `Derived` objects. Note that we used the  
`Base` type in our array declaration. The Derived class can be converted to the  
`Base` class, because it inherits from it. The opposite is not `true`. The only  
way to have defferent objects in one array is to use a type which is shared by  
all objects.  

```java
for (Base obj : objs) {

    obj.showInfo();
}
```

We traverse the array and call `showInfo` on all objects in the array. The  
method to be called is determined at runtime.  


With the `super` keyword, it is possible to call the overridden method.

```java
package com.zetcode;

class Base {

    public void showInfo() {

        System.out.println("This is Base class");
    }
}

class Derived extends Base {

    @Override
    public void showInfo() {

        System.out.println("This is Derived class");
    }

    public void showBaseInfo() {

        super.showInfo();
    }
}

public class Overriding2 {

    public static void main(String[] args) {

        Derived d = new Derived();
        d.showBaseInfo();
    }
}
```

In the example, we call the `showInfo` of the `Base` class with super.

```java
public void showBaseInfo() {

    super.showInfo();
}
```

Here we call the immediate parent's `showInfo` method.

## The final methods

A `final` method cannot be overriden or hidden by derived classes. This is used  
to prevent unexpected behavior from a subclass altering a method that may be  
crucial to the function or consistency of the class.  

```java
package com.zetcode;

class Base {

    public void f1() {

        System.out.println("f1 of the Base");
    }

    public final void f2() {

        System.out.println("f2 of the Base");
    }
}

class Derived extends Base {

    @Override
    public void f1() {

        System.out.println("f1 of the Derived");
    }

//    @Override
//    public void f2() {
//
//        System.out.println("f2 of the Derived");
//    }
}


public class FinalMethods {

    public static void main(String[] args) {

        Base b = new Base();
        b.f1();
        b.f2();

        Derived d = new Derived();
        d.f1();
        d.f2();
    }
}
```

In this example we have a final method `f2` in the `Base` class. This method  
cannot be overriden.

```java
public final void f2() {

    System.out.println("f2 of the Base");
}
```

The `f2` method is declared to be final. No overloading is possible.  

```java
@Override
public void f1() {

    System.out.println("f1 of the Derived");
}
```

In the `Derived` class, we can override the `f1` method of the `Base` class. We  
also use the `@Override` annotation to inform the compiler that we are  
overriding a method.  

```
//    @Override
//    public void f2() {
//
//        System.out.println("f2 of the Derived");
//    }
```

These lines are commented, because otherwise the code example would not compile.  
The compiler would give the following error: `Exception` in thread "main"  
`java.lang.VerifyError`: class com.zetcode.Derived overrides final method `f2`.  

```java
d.f2();
```

Since it is not possible to override a `final` method, the above line will call  
the `f2` method of the `Base` class.  
