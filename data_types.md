## Data types

A data type is a set of values and the allowable operations on those values.  

Java programming language is a statically typed language. It means that every  
variable and every expression has a type that is known at compile time. Java  
language is also a strongly typed language because types limit the values that a  
variable can hold or that an expression can produce, limit the operations  
supported on those values, and determine the meaning of the operations.  

Strong static typing helps detect errors at compile time. Variables in  
dynamically typed languages like Ruby or Python can receive different data types  
over the time. In Java, once a variable is declared to be of a certain data  
type, it cannot hold values of other data types.  

There are two fundamental data types in Java: primitive types and reference
types. 

Primitive types:

- boolean
- char
- byte
- short
- int
- long
- float
- double


There is a specific keyword for each of these types in Java. Primitive types are  
not objects in Java. Primitive data types cannot be stored in Java collections  
which work only with objects. They can be placed into arrays instead.  

The reference types:

- class types
- interface types
- array types

There is also a special null type which represents a non-existing value.  

In Ruby programming language, everything is an object. Even basic data types.  

```ruby
#!/usr/bin/ruby

4.times { puts "Ruby" }
```

This Ruby script prints four times "Ruby" string to the console. We call a times  
method on the 4 number. This number is an object in Ruby.  

Java has a different approach. It has primitive data types and wrapper classes.  
Wrapper classes transform primitive types into objects.  

## Boolean values

In Java the boolean data type is a primitive data type having one of two values:  
`true` or `false`.

```java
import java.util.Random;

void main() {

    String name = "";
    Random r = new Random();
    boolean male = r.nextBoolean();

    if (male == true) {

        name = "Robert";
    }

    if (male == false) {

        name = "Victoria";
    }

    System.out.format("We will use name %s%n", name);
    System.out.println(9 > 8);
}
```

The program uses a random number generator to simulate our case.


## Integers

Integers are a subset of the real numbers. They are written without a fraction  
or a decimal component. 

Integers fall within a set `Z = {..., -2, -1, 0, 1, 2,...}`. Integers are infinite.  

Computers can practically work only with a subset of integer values, because  
computers have finite capacity. Integers are used to count discrete entities. We  
can have 3, 4, or 6 humans, but we cannot have 3.33 humans. We can have 3.33  
kilograms, 4.564 days, or 0.4532 kilometers.  


| Type  | Size     | Range                                   |
|-------|----------|-----------------------------------------|
| byte  | 8 bits   | -128 to 127                             |
| short | 16 bits  | -32,768 to 32,767                       |
| char  | 16 bits  | 0 to 65,535                             |
| int   | 32 bits  | -2,147,483,648 to 2,147,483,647         |
| long  | 64 bits  | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |

Table: Integer types in Java

These integer types may be used according to our needs. We can then use the byte  
type for a variable that stores the number of children a woman gave birth to.  
The oldest verified person died at 122, therefore we would probably choose at  
least the short type for the age variable. This will save us some memory.  

Integer literals may be expressed in decimal, hexadecimal, octal, or binary  
notations. If a number has an ASCII letter L or l suffix, it is of type long.  
Otherwise it is of type int. The capital letter L is preferred for specifying  
long numbers, since lowercase l can be easily confused with number 1.  

```
int a = 34;
byte b = 120;
short c = 32000;
long d = 45000;
long e = 320000L;
```

We have five assignments. Values 34, 120, 32000, and 45000 are integer literals  
of type `int`. There are no integer literals for `byte` and `short` types. If  
the values fit into the destination type, the compiler does not complain and  
performs a conversion automatically. For long numbers smaller than  
`Integer.MAX_VALUE`, the `L` suffix is optional.  

```
long x = 2147483648L;
long y = 2147483649L;
```

For long numbers larger than `Integer.MAX_VALUE`, we must add the `L` suffix.  

When we work with integers, we deal with discrete items. For instance, we can  
use integers to count apples.  

```java
void main() {

    int baskets = 16;
    int applesInBasket = 24;

    int total = baskets * applesInBasket;

    System.out.format("There are total of %d apples%n", total);
}
```

In our program, we count the total amount of apples. We use the multiplication
operation.

```java
int baskets = 16;
int applesInBasket = 24;
```

The number of baskets and the number of apples in each basket are integer values.

```java
int total = baskets * applesInBasket;
```

Multiplying those values we get an integer, too.  


Integers can be specified in four different notations in Java: decimal, octal,  
hexadecimal, and binary. Decimal numbers are used normally as we know them.  
Octal numbers are preceded with a 0 character and followed by octal numbers.  
Hexadecimal numbers are preceded with `0x` characters and followed by  
hexadecimal numbers. Binary numbers start with `0b` and are followed by binary  
numbers (zeroes and ones).  


```java
void main() {

    int n1 = 31;
    int n2 = 0x31;
    int n3 = 031;
    int n4 = 0b1001;

    System.out.println(n1);
    System.out.println(n2);
    System.out.println(n3);
    System.out.println(n4);
}
```

We have four integer variables. Each of the variables is assigned a value with a  
different integer notation.  

```java
int n1 = 31;
int n2 = 0x31;
int n3 = 031;
int n4 = 0b1001;
```

The first is decimal, the second hexadecimal, the third octal, and the fourth  
binary.


Big numbers are difficult to read. If we have a number like 245342395423452, we  
find it difficult to read it quickly. Outside computers, big numbers are  
separated by spaces or commas. 

The underscore cannot be used at the beginning or end of a number, adjacent to a  
decimal point in a floating point literal, and prior to an `F` or `L` suffix.  

```java
void main() {

    long a = 23482345629L;
    long b = 23_482_345_629L;

    System.out.println(a == b);
}
```

This code sample demonstrates the usage of underscores in Java.  

```java
long a = 23482345629L;
long b = 23_482_345_629L;
```

We have two identical `long` numbers. In the second one we separate every three  
digits in a number. Comparing these two numbers we receive a boolean `true`. The  
`L` suffix tells the compiler that we have a `long` number literal.  

Java `byte`, `short`, `int` and `long` types are used do represent fixed  
precision numbers. This means that they can represent a limited amount of  
integers. The largest integer number that a `long` type can represent is  
9223372036854775807. If we deal with even larger numbers, we have to use the  
`java.math.BigInteger` class. It is used to represent immutable arbitrary  
precision integers. Arbitrary precision integers are only limited by the amount  
of computer memory available.  

```java
void main() {

    System.out.println(Long.MAX_VALUE);

    BigInteger b = new BigInteger("92233720368547758071");
    BigInteger c = new BigInteger("52498235605326345645");

    BigInteger a = b.multiply(c);

    System.out.println(a);
}
```

With the help of the `java.math.BigInteger` class, we multiply two very large  
numbers.  

## Arithmetic overflow

An arithmetic overflow is a condition that occurs when a calculation produces a  
result that is greater in magnitude than that which a given register or storage  
location can store or represent.  

```java
void main() {

    byte a = 126;

    System.out.println(a);
    a++;

    System.out.println(a);
    a++;

    System.out.println(a);
    a++;

    System.out.println(a);
}
```

## Floating point numbers

Real numbers measure continuous quantities, like weight, height, or speed.  
Floating point numbers represent an approximation of real numbers in computing.  
In Java we have two primitive floating point types: `float` and `double`.  

The `float` is a single precision type which store numbers in 32 bits. The  
`double` is a double precision type which store numbers in 64 bits. These two  
types have fixed precision and cannot represent exactly all real numbers. In  
situations where we have to work with precise numbers, we can use the  
`BigDecimal` class.  

Floating point numbers with an `F/f` suffix are of type `float`, `double`  
numbers have `D/d` suffix. The suffix for `double` numbers is optional.  

Let's say a sprinter for 100m ran 9.87s. What is his speed in km/h?  

```java
void main() {

    float distance;
    float time;
    float speed;

    distance = 0.1f;

    time = 9.87f / 3600;

    speed = distance / time;

    System.out.format("The average speed of a sprinter is %f km/h%n", speed);
}
```

In this example, it is necessary to use floating point values. The low precision  
of the `float` data type does not pose a problem in this case.  


The `float` and `double` types are inexact.

```java
void main() {

    double a = 0.1 + 0.1 + 0.1;
    double b = 0.3;

    System.out.println(a);
    System.out.println(b);

    System.out.println(a == b);
}
```

The code example illustrates the inexact nature of the floating point values.  

When we work with money, currency, and generally in business applications, we  
need to work with precise numbers. The rounding errors of the basic floating  
point types are not acceptable.  

```java
void main() {

    float c = 1.46f;
    float sum = 0f;

    for (int i=0; i<100_000; i++) {

        sum += c;
    }

    System.out.println(sum);
}
```

The `1.46f` represents 1 euro and 46 cents. We create a sum from 100000 such  
amounts.  

```java
for (int i=0; i<100_000; i++) {

    sum += c;
}
```

In this loop, we create a sum from 100000 such amounts of money.

```
$ java CountingMoney.java
146002.55
```

The calculation leads to an error of 2 euros and 55 cents.

To avoid this margin error, we utilize the `BigDecimal` class. It is used to  
hold immutable, arbitrary precision signed decimal numbers.  

```java
import java.math.BigDecimal;

void main() {

    BigDecimal c = new BigDecimal("1.46");
    BigDecimal sum = new BigDecimal("0");

    for (int i=0; i<100_000; i++) {

        sum = sum.add(c);
    }

    System.out.println(sum);
}
```


Java supports the scientific syntax of the floating point values. Also known as  
exponential notation, it is a way of writing numbers too large or small to be  
conveniently written in standard decimal notation.  

```java
import java.math.BigDecimal;
import java.text.DecimalFormat;

void main() {

    double n = 1.235E10;
    DecimalFormat dec = new DecimalFormat("#.00");

    System.out.println(dec.format(n));

    BigDecimal bd = new BigDecimal("1.212e-19");

    System.out.println(bd.toEngineeringString());
    System.out.println(bd.toPlainString());
}
```

We define two floating point values using the scientific notation.  

## Enumerations

An enum type is a special data type that enables for a variable to be a set of  
predefined constants. A variable that has been declared as having an enumerated  
type can be assigned any of the enumerators as a value. Enumerations make the  
code more readable. Enumerations are useful when we deal with variables that can  
only take one out of a small set of possible values.  

```java
enum Days {

    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY,
    SUNDAY
}

void main() {

    Days day = Days.MONDAY;

    if (day == Days.MONDAY) {

        System.out.println("It is Monday");
    }

    System.out.println(day);

    for (Days d : Days.values()) {

        System.out.println(d);
    }
}
```

In our code example, we create an enumeration for week days.  

It is possible to give some values to the enumeration constants.  

```java
enum Season {

    SPRING(10),
    SUMMER(20),
    AUTUMN(30),
    WINTER(40);

    private int value;

    private Season(int value) {
        this.value = value;
    }

    public int getValue() {

        return value;
    }
}

void main() {

    for (Season season : Season.values()) {
        System.out.println(season + " " + season.getValue());
    }
}
```

The example contains a Season enumeration which has four constants.

## Strings and chars

A String is a data type representing textual data in computer programs. A string  
in Java is a sequence of characters. A char is a single character. Strings are  
enclosed by double quotes.  

```java
void main() {

    String word = "ZetCode";

    char c = word.charAt(0);
    char d = word.charAt(3);

    System.out.println(c);
    System.out.println(d);
}
```

The program prints Z character to the terminal.


## Arrays

Array is a data type which handles a collection of elements. Each of the  
elements can be accessed by an index. All the elements of an array must be of  
the same data type.  

```java
void main() {

    int[] numbers = new int[5];

    numbers[0] = 3;
    numbers[1] = 2;
    numbers[2] = 1;
    numbers[3] = 5;
    numbers[4] = 6;

    int len = numbers.length;

    for (int i = 0; i < len; i++) {

        System.out.println(numbers[i]);
    }
}
```

In this example, we declare an array, fill it with data and then print the  
contents of the array to the console.  


## Java wrapper classes
 
Wrapper classes are object representations of primitive data types. Wrapper  
classes are used to represent primitive values when an Object is required. For  
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


## The null type

Java has a special `null` type. The type has no name. As a consequence, it is  
impossible to declare a variable of the `null` type or to cast to the `null`  
type. The `null` represents a `null` reference, one that does not refer to any  
object. The `null` is the default value of reference-type variables. Primitive  
types cannot be assigned a `null` literal.  

In different contexts, the `null` means an absence of an object, an unknown  
value, or an uninitialized state.  

```java
import java.util.Random;

String getName() {

    Random r = new Random();
    boolean n = r.nextBoolean();

    if (n == true) {

        return "John";
    } else {

        return null;
    }
}

void main() {

    String name = getName();
    System.out.println(name);
    System.out.println(null == null);

    if ("John".equals(name)) {

        System.out.println("His name is John");
    }
}
```

We work with the `null` value in the program.


## Default values

Uninitialized fields are given default values by the compiler. Final fields and  
local variables must be initialized by developers.  

The following table shows the default values for different types.  

Here is the data you provided in a markdown table format:  

| Data type | Default value |
|-----------|---------------|
| byte      | 0             |
| char      | '\u0000'      |
| short     | 0             |
| int       | 0             |
| long      | 0L            |
| float     | 0f            |
| double    | 0d            |
| Object    | null          |
| boolean   | false         |

Table: Default values for uninitialized instance variables  

The next example will print the default values of the uninitialized instance  
variables. An instance variable is a variable defined in a class for which each  
instantiated object of the class has a separate copy.  

```java
byte b;
char c;
short s;
int i;
float f;
double d;
String str;
Object o;

void main() {

    System.out.println(b);
    System.out.println(c);
    System.out.println(s);
    System.out.println(i);
    System.out.println(f);
    System.out.println(d);
    System.out.println(str);
    System.out.println(o);
}
```

In the example, we declare eight member fields. They are not initialized. The  
compiler will set a default value for each of the fields.  

## Type conversions

We often work with multiple data types at once. Converting one data type to  
another one is a common job in programming. The term type conversion refers to  
changing of an entity of one data type into another. In this section, we deal  
with conversions of primitive data types. Reference type conversions will be  
mentioned later in this chapter. The rules for conversions are complex; they are  
specified in chapter 5 of the Java language specification.  

There are two types of conversions: *implicit* and *explicit*. Implicit type  
conversion, also known as coercion, is an automatic type conversion by the  
compiler. In explicit conversion the programmer directly specifies the  
converting type inside a pair of round brackets. Explicit conversion is called  
type casting.  

Conversions happen in different contexts: assignments, expressions, or   
method invocations.

```java
int x = 456;
long y = 34523L;
float z = 3.455f;
double w = 6354.3425d;
```

In these four assignments, no conversion takes place. Each of the variables is  
assigned a literal of the expected type.  

```java
int x = 345;
long y = x;

float m = 22.3354f;
double n = m;
```

In this code two conversions are performed by Java compiler implicitly.  
Assigning a variable of a smaller type to a variable of a larger type is legal.  
The conversion is considered safe, as no precision is lost. This kind of  
conversion is called implicit widening conversion.  

```java
long x = 345;
int y = (int) x;

double m = 22.3354d;
float n = (float) m;
```

Assigning variables of larger type to smaller type is not legal in Java. Even if  
the values themselves fit into the range of the smaller type. In this case it is  
possible to loose precision. To allow such assignments, we have to use the type  
casting operation. This way the programmer says that he is doing it on purpose  
and that he is aware of the fact that there might be some precision lost. This  
kind of conversion is called explicit narrowing conversion.  

```java
byte a = 123;
short b = 23532;
```

In this case, we deal with a specific type of assignment conversion. 123 and  
23532 are integer literals, the a, b variables are of byte and short type. It is  
possible to use the casting operation, but it is not required. The literals can  
be represented in their variables on the left side of the assignment. We deal  
with implicit narrowing conversion.  

```java
private static byte calc(byte x) {
...
}

byte b = calc((byte) 5);
```
The above rule only applies to assignments. When we pass an integer literal to a  
method that expects a byte, we have to perform the casting operation.  

## Numeric promotions

Numeric promotion is a specific type of an implicit type conversion. It takes  
place in arithmetic expressions. Numeric promotions are used to convert the  
operands of a numeric operator to a common type so that an operation can be  
performed.  

```java
int x = 3;
double y = 2.5;
double z = x + y;
```

In the third line we have an addition expression. The `x` operand is int, the `y`  
operand is double. The compiler converts the integer to double value and adds  
the two numbers. The result is a double. It is a case of implicit widening  
primitive conversion.  

```java
byte a = 120;
a = a + 1; // compilation error
```

This code leads to a compile time error. In the right side of the second line,  
we have a byte variable a and an integer literal 1. The variable is converted to  
integer and the values are added. The result is an integer. Later, the compiler  
tries to assign the value to the a variable. Assigning larger types to smaller  
types is not possible without an explicit cast operator. Therefore we receive a  
compile time error.  

```java
byte a = 120;
a = (byte) (a + 1);
```

This code does compile. Note the usage of round brackets for the `a + 1`  
expression. The (byte) casting operator has a higher precedence than the  
addition operator. If we want to apply the casting on the whole expression, we  
have to use round brackets.  

```java
byte a = 120;
a += 5;
```

Compound operators perform implicit conversions automatically.  

```java
short r = 21;
short s = (short) -r;
```

Applying the `+` or `-` unary operator on a variable a unary numberic promotion  
is performed. The short type is promoted to int type. Therefore we must use the  
casting operator for the assignment to pass.  

```java
byte u = 100;
byte v = u++;
```

In case of the unary increment `++`, decrement `--` operators, no conversion is  
done. The casting is not necessary.  

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
