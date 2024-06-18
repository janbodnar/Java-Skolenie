# Wrapper types 

Wrapper classes are object representations of primitive data types. Wrapper  
classes are used to represent primitive values when an `Object` is required. For  
example, Java collections only work with objects. They cannot take primitive  
types. Wrapper classes also include some useful methods. For example, they  
include methods for doing data type conversions. Placing primitive types into  
wrapper classes is called boxing. The reverse process is called unboxing.  

As a general rule, we use wrapper classes when we have some reason for it.  
Otherwise, we use primitive types. Wrapper classes are immutable. Once they are  
created, they cannot be changed. Primitive types are faster than boxed types. In  
scientific computing and other large scale number processing, wrapper classes  
may cause significant performance hit.  

Here is the markdown table you requested:

| Primitive type | Wrapper class | Constructor arguments |
| --- | --- | --- |
| byte | Byte | byte or String |
| short | Short | short or String |
| int | Integer | int or String |
| long | Long | long or String |
| float | Float | float, double or String |
| double | Double | double or String |
| char | Character | char |
| boolean | Boolean | boolean or String |

Table: Primitive types and their wrapper class equivalents

The Integer class wraps a value of the primitive type int in an object. It  
contains constants and methods useful when dealing with an int.  

```java
void main() {

    int a = 55;
    Integer b = new Integer(a);

    int c = b.intValue();
    float d = b.floatValue();

    String bin = Integer.toBinaryString(a);
    String hex = Integer.toHexString(a);
    String oct = Integer.toOctalString(a);

    System.out.println(a);
    System.out.println(b);
    System.out.println(c);
    System.out.println(d);

    System.out.println(bin);
    System.out.println(hex);
    System.out.println(oct);
}
```

This example works with the `Integer` wrapper class.  

Collections are powerful tools for working with groups of objects. Primitive  
data types cannot be placed into Java collections. After we box the primitive  
values, we can put them into collections.  

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    List<Number> ls = new ArrayList<>();

    ls.add(1342341);
    ls.add(new Float(34.56));
    ls.add(235.242);
    ls.add(new Byte("102"));
    ls.add(new Short("1245"));

    for (Number n : ls) {

        System.out.println(n.getClass());
        System.out.println(n);
    }
}
```

In the example, we put various numbers into a `ArrayList`. An `ArrayList` is a   
dynamic, resizable array.  

## Java boxing

Converting from primitive types to object types is called boxing. Unboxing is  
the opposite operation. It is converting of object types back into primitive  
types.  

```java
void main() {

    long a = 124235L;

    Long b = new Long(a);
    long c = b.longValue();

    System.out.println(c);
}
```

In the code example, we box a long value into a Long object and vice versa.  

```java
Long b = new Long(a);
```

This line performs boxing.

```java
long c = b.longValue();
```

In this line we do unboxing.


## Autoboxing

Autoboxing is automatic conversion between primitive types and their  
corresponding object wrapper classes. Autoboxing makes programming easier. The  
programmer does not need to do the conversions manually.  

Automatic boxing and unboxing is performed when one value is primitive type and  
other is wrapper class in:  

- assignments
- passing parameters to methods
- returning values from methods
- comparison operations
- arithmetic operations


```java
Integer i = new Integer(50);

if (i < 100) {
   ...
}
```

Inside the square brackets of the if expression, an `Integer` is compared with  
an `int`. The `Integer` object is transformed into the primitive `int` type and  
compared with the 100 value. Automatic unboxing is done.  

```java
int cube(int x) {

    return x * x * x;
}

void main() {

    Integer i = 10;
    int j = i;

    System.out.println(i);
    System.out.println(j);

    Integer a = cube(i);
    System.out.println(a);
}
```

Automatic boxing and automatic unboxing is demonstrated in this code example.

```java
Integer i = 10;
```

The Java compiler performs automatic boxing in this code line. An `int` value is  
boxed into the `Integer` type.  

```java
int j = i;
```

Here an automatic unboxing takes place.  

```java
Integer a = cube(i);
```

When we pass an `Integer` to the cube method, automatic unboxing is done. When  
we return the computed value, automatic boxing is performed, because an `int` is  
transformed back to the `Integer`.  

Java language does not support operator overloading. When we apply arithmetic  
operations on wrapper classes, automatic boxing is done by the compiler.  

```java
void main() {

    Integer a = new Integer(5);
    Integer b = new Integer(7);

    Integer add = a + b;
    Integer mul = a * b;

    System.out.println(add);
    System.out.println(mul);
}
```

We have two `Integer` values. We perform addition and multiplication operations  
on these two values.  

```java
Integer add = a + b;
Integer mul = a * b;
```

Unlike languages like Ruby, C#, Python, D or C++, Java does not have operator  
overloading implemented. In these two lines, the compiler calls the `intValue`  
methods and converts the wrapper classes to ints and later wraps the outcome  
back to an Integer by calling the `valueOf` method.  

## Autoboxing and object interning

*Object intering* is storing only one copy of each distinct object. The object  
must be immutable. The distinct objects are stored in an intern pool. In Java,  
when primitive values are boxed into a wrapper object, certain values (any  
boolean, any byte, any char from 0 to 127, and any short or int between -128 and  
127) are interned, and any two boxing conversions of one of these values are  
guaranteed to result in the same object.  

According to the Java language specification, these are minimal ranges. So the  
behaviour is implementation dependent. Object intering saves time and space.  
Objects obtained from literals, autoboxing and `Integer.valueOf` are interned  
objects while those constructed with new operator are always distinct objects.  

The object intering has some important consequences when comparing wrapper  
classes. The `==` operator compares reference identity of objects while the  
equals method compares values.  

```java
void main() {

    Integer a = 5; // new Integer(5);
    Integer b = 5; // new Integer(5);

    System.out.println(a == b);
    System.out.println(a.equals(b));
    System.out.println(a.compareTo(b));

    Integer c = 155;
    Integer d = 155;

    System.out.println(c == d);
    System.out.println(c.equals(d));
    System.out.println(c.compareTo(d));
}
```

The example compares some `Integer` objects.

```java
Integer a = 5; // new Integer(5);
Integer b = 5; // new Integer(5);
```

Two integers are boxed into Integer wrapper classes.

```java
System.out.println(a == b);
System.out.println(a.equals(b));
System.out.println(a.compareTo(b));
```

Three different ways are used to compare the values. The `==` operator compares  
the reference identity of two boxed types. Because of the object interning, the  
operation results in true. If we used the new operator, two distinct objects  
would be created and the `==` operator would return false. The `equals` method  
compares the two `Integer` objects numerically. It returns a boolean `true` or  
`false` (a `true` in our case.)  

Finally, the `compareTo` method also compares the two objects numerically. It  
returns the value 0 if this `Integer` is equal to the argument `Integer`; a  
value less than 0 if this `Integer` is numerically less than the argument  
`Integer`; and a value greater than 0 if this `Integer` is numerically greater  
than the argument `Integer`.  

```java
Integer c = 155;
Integer d = 155;
```

We have another two boxed types. However, these values are greater than the  
maximum value interned (127); therefore, two distinct objects are created. This  
time the `==` operator yields false.  



## Boxing, unboxing conversions

Boxing conversion converts expressions of primitive type to corresponding  
expressions of wrapper type. Unboxing conversion converts expressions of wrapper  
type to corresponding expressions of primitive type. Conversions from `boolean`  
to `Boolean` or from `byte` to `Byte` are examples of boxing conversions. The  
reverse conversions, e.g. from `Boolean` to `boolean` or from Byte to byte are  
examples of unboxing conversions.  

```java
Byte b = 124;
byte c = b;
```

In the first code line, automatic boxing conversion is performed by the Java  
compiler. In the second line, an unboxing conversion is done.  

```java
private static String checkAge(Short age) {
...
}

String r = checkAge((short) 5);
```

Here we have boxing conversion in the context of a method invocation. We pass a  
short type to the method which expects a Short wrapper type. The value is boxed.  

```java
Boolean gameOver = new Boolean("true");
if (gameOver) {
    System.out.println("The game is over");
}
```

This is an example of an unboxing conversion. Inside the if expression, the  
booleanValue method is called. The method returns the value of a `Boolean` object  
as a `boolean` primitive.  

## Object reference conversion

Objects, interfaces, and arrays are reference data types. Any reference can be  
cast to the `Object`. `Object` type determines which method is used at runtime.  
Reference type determines which overloaded method will be used at compile time.  

An interface type may only be converted to an interface type or to `Object`. If  
the new type is an interface, it must be a super interface of the old type. A  
class type may be converted to a class type or to an interface type. If  
converting to a class type, the new type must be a super class of the old type.  
If converting to an interface type, the old class must implement the interface.  
An array may be converted to the class `Object`, to the interface Cloneable or  
Serializable, or to an array.  

There are two types of reference variable casting: downcasting and upcasting.  
Upcasting (generalization or widening) is casting from a child type to a parent  
type. We are casting an individual type to a common type. Downcasting  
(specialization or narrowing) is casting from a parent type to a child type. We  
are casting a common type to an individual type.  

Upcasting narrows the list of methods and properties available to an object, and  
downcasting can extend it. Upcasting is safe, but downcasting involves a type  
check and can throw a `ClassCastException`.  

```java
import java.util.Random;

class Animal {}
class Mammal extends Animal {}
class Dog extends Animal {}
class Cat extends Animal {}

void main() {

    // upcasting
    Animal animal = new Dog();
    System.out.println(animal);

    // ClassCastException
    // Mammal mammal = (Mammal) new Animal();

    var returned = getRandomAnimal();

    if (returned instanceof Cat) {

        Cat cat = (Cat) returned;
        System.out.println(cat);
    } else if (returned instanceof Dog) {

        Dog dog = (Dog) returned;
        System.out.println(dog);
    } else if (returned instanceof Mammal) {

        Mammal mammal = (Mammal) returned;
        System.out.println(mammal);
    } else {

        Animal animal2 = returned;
        System.out.println(animal2);
    }
}

Animal getRandomAnimal() {

    int val = new Random().nextInt(4) + 1;

    Animal anim = switch (val) {

        case 2 -> new Mammal();
        case 3 -> new Dog();
        case 4 -> new Cat();
        default -> new Animal();
    };

    return anim;
}
```

The example performs reference type conversions.

```java
// upcasting
Animal animal = new Dog();
System.out.println(animal);
```

We cast from a child type `Dog` to a parent type `Animal`. This is upcasting and  
it is always safe.  

```java
// ClassCastException
// Mammal mammal = (Mammal) new Animal();
```

Downcasting from an `Animal` to a `Mammal` leads to a `ClassCastException`.  

```java
var returned = getRandomAnimal();

if (returned instanceof Cat) {

    Cat cat = (Cat) returned;
    System.out.println(cat);
} else if (returned instanceof Dog) {

    Dog dog = (Dog) returned;
    System.out.println(dog);
} else if (returned instanceof Mammal) {

    Mammal mammal = (Mammal) returned;
    System.out.println(mammal);
} else {

    Animal animal2 = returned;
    System.out.println(animal2);
}
```

In order to perform legal downcasting, we need to check the type of the object  
with the instanceof operator first.  

```java
Animal getRandomAnimal() {

    int val = new Random().nextInt(4) + 1;

    Animal anim = switch (val) {

        case 2 -> new Mammal();
        case 3 -> new Dog();
        case 4 -> new Cat();
        default -> new Animal();
    };

    return anim;
}
```

The `getRandomAnimal` returns a random animal using Java's swith expression.  



## String conversions

Performing string conversions between numbers and strings is very common in  
programming. The casting operation is not allowed because the strings and  
primitive types are fundamentally different types. There are several methods for  
doing string conversions. There is also an automatic string conversion for the  
`+` operator.  
  

```java
String s = (String) 15; // compilation error
int i = (int) "25"; // compilation error
```

It is not possible to cast between numbers and strings. Instead, we have various  
methods for doing conversion between numbers and strings.  

```java
short age = Short.parseShort("35");
int salary = Integer.parseInt("2400");
float height = Float.parseFloat("172.34");
double weight = Double.parseDouble("55.6");
```

The parse methods of the wrapper classes convert strings to primitive types.  

```java
Short age = Short.valueOf("35");
Integer salary = Integer.valueOf("2400");
Float height = Float.valueOf("172.34");
Double weight = Double.valueOf("55.6");
```

The `valueOf` method returns the wrapper classes from primitive types.  

```java
int age = 17;
double weight = 55.3;
String v1 = String.valueOf(age);
String v2 = String.valueOf(weight);
```

The String class has a `valueOf` method for converting various types to strings.  

Automatic string conversions take place when using the `+` operator and one  
operator is a string, the other operator is not a string. The non-string operand  
to the `+` is converted to a string.  

```java
void main() {

    String name = "Jane";
    short age = 17;

    System.out.println(name + " is " +  age + " years old.\n");
}
```

In the example, we have a `String` data type and a `short` data type. The two  
types are concatenated using the `+` operator into a sentence.  

```java
System.out.println(name + " is " +  age + " years old.");
```

In the expression, the age variable is converted to a `String` type.  









