# Operators

An *operator* is a special symbol which indicates a certain process is carried  
out. Operators in programming languages are taken from mathematics. Programmers  
work with data. The operators are used to process data. An operand is one of the  
inputs (arguments) of an operator.  

*Expressions* are constructed from operands and operators. The operators of an  
expression indicate which operations to apply to the operands. The order of  
evaluation of operators in an expression is determined by the precedence and  
associativity of the operators.  

An operator usually has one or two operands. Those operators that work with only  
one operand are called unary operators. Those who work with two operands are  
called binary operators. There is also one ternary operator `?:` which works with  
three operands.  

Certain operators may be used in different contexts. For example the `+` operator.  
It can be used in different cases. It adds numbers, concatenates strings, or  
indicates the sign of a number. We say that the operator is overloaded.  

## Sign operators

There are two sign operators: `+` and `-`. They are used to indicate or change  
the sign of a value.

```java
void main() {

    System.out.println(2);
    System.out.println(+2);
    System.out.println(-2);
}
```

The `+` and `-` signs indicate the sign of a value. The plus sign can be used to  
signal that we have a positive number. It can be omitted and it is mostly done  
so.

```java
void main() {

    int a = 1;

    System.out.println(-a);
    System.out.println(-(-a));
}
```

The minus sign changes the sign of a value.

## Assignment operator

The assignment operator `= `assigns a value to a variable. A variable is a  
placeholder for a value. In mathematics, the `=` operator has a different  
meaning. In an equation, the `=` operator is an equality operator. The left side  
of the equation is equal to the right one.  

```java
int x = 1;
```

Here we assign a number to the `x` variable.  

```java
x = x + 1;
```

This expression does not make sense in mathematics, but it is legal in  
programming. The expression adds 1 to the x variable. The right side is equal to  
2 and 2 is assigned to `x`.  

```java
3 = x;
```


This code line results in syntax error. We cannot assign a value to a literal.

## Concatenating strings

In Java the `+` operator is also used to concatenate strings.

```java
void main() {

    System.out.println("Return " + "of " + "the king.");
    System.out.println("Return".concat(" of").concat(" the king."));
}
```

We join three strings together.

```java
System.out.println("Return " + "of " + "the king.");
```

Strings are joined with the `+` operator.

```java
System.out.println("Return".concat(" of").concat(" the king."));
```

An alternative method for concatenating strings is the concat method.


## Increment and decrement operators

Incrementing or decrementing a value by one is a common task in programming.

Java has two convenient operators for this: `++` and `--`.

```java
x++;
x = x + 1;
...
y--;
y = y - 1;
```

The above two pairs of expressions do the same.

```java
void main() {

    int x = 6;

    x++;
    x++;

    System.out.println(x);

    x--;
    System.out.println(x);
}
```

In the above example, we demonstrate the usage of both operators.

```java
int x = 6;

x++;
x++;
```

We initiate the `x` variable to 6. Then we increment `x` two times. Now the  
variable equals to 8.  

```java
x--;
```

We use the decrement operator. Now the variable equals to 7.


## Arithmetic operators

The following is a table of arithmetic operators in Java.

Here is the data you provided in a markdown table format:

| Symbol | Name          |
|--------|---------------|
| +      | Addition      |
| -      | Subtraction   |
| *      | Multiplication|
| /      | Division      |
| %      | Remainder     |



The following example shows arithmetic operations.

```java
void main() {

    int a = 10;
    int b = 11;
    int c = 12;

    int add = a + b + c;
    int sb = c - a;
    int mult = a * b;
    int div = c / 3;
    int rem = c % a;

    System.out.println(add);
    System.out.println(sb);
    System.out.println(mult);
    System.out.println(div);
    System.out.println(rem);
}
```

In the preceding example, we use addition, subtraction, multiplication,  
division, and remainder operations. This is all familiar from the mathematics.  

```java
int rem = c % a;
```

The `%` operator is called the remainder or the modulo operator. It finds the  
remainder of division of one number by another. For example, `9 % 4`, 9 modulo 4  
is 1, because 4 goes into 9 twice with a remainder of 1.  

Next we show the distinction between integer and floating point division.  

```java
void main() {

    int c = 5 / 2;
    System.out.println(c);

    double d = 5 / 2.0;
    System.out.println(d);
}
```

In the preceding example, we divide two numbers.  

```java
int c = 5 / 2;
```

In this code, we have done integer division. The returned value of the division  
operation is an integer. When we divide two integers the result is an integer.  

```java
double d = 5 / 2.0;
```

If one of the values is a `double` or a `float`, we perform a floating point  
division. In our case, the second operand is a double so the result is a double.  


## Boolean operators

In Java we have three logical operators. The boolean keyword is used to declare  
a Boolean value.  

Here is the data you provided in a markdown table format:  

| Symbol | Name        |
|--------|-------------|
| &&     | logical and |
| \|\|   | logical or  |
| !      | negation    |


Boolean operators are also called logical.  

```java
void main() {

    int x = 3;
    int y = 8;

    System.out.println(x == y);
    System.out.println(y > x);

    if (y > x) {

        System.out.println("y is greater than x");
    }
}
```

Many expressions result in a boolean value. For instance, boolean values are  
used in conditional statements.  

```java
System.out.println(x == y);
System.out.println(y > x);
```

Relational operators always result in a boolean value. These two lines print  
false and true.  

```java
if (y > x) {

    System.out.println("y is greater than x");
}
```

The body of the if statement is executed only if the condition inside the  
parentheses is met. The `y > x` returns true, so the message "y is greater than x"  
is printed to the terminal.

The `true` and `false` keywords represent boolean literals in Java.  

```java
void main() {

    boolean a = true && true;
    boolean b = true && false;
    boolean c = false && true;
    boolean d = false && false;

    System.out.println(a);
    System.out.println(b);
    System.out.println(c);
    System.out.println(d);
}
```

The code example shows the logical and `&&` operator. It evaluates to true only  
if both operands are true.  


The logical or `||` operator evaluates to `true` if either of the operands is  
`true`.  

```java
void main() {

    boolean a = true || true;
    boolean b = true || false;
    boolean c = false || true;
    boolean d = false || false;

    System.out.println(a);
    System.out.println(b);
    System.out.println(c);
    System.out.println(d);
}
```

If one of the sides of the operator is `true`, the outcome of the operation is
`true`.



The negation operator `!` makes `true` `false` and false `true`.

```java
void main() {

    System.out.println(! true);
    System.out.println(! false);
    System.out.println(! (4 < 3));
}
```

The example shows the negation operator in action.  


The `||`, and `&&` operators are *short circuit* evaluated. Short circuit  
evaluation means that the second argument is only evaluated if the first  
argument does not suffice to determine the value of the expression: when the  
first argument of the logical and evaluates to `false`, the overall value must  
be false; and when the first argument of logical or evaluates to true, the  
overall value must be `true`. Short circuit evaluation is used mainly to improve  
performance.  

An example may clarify this a bit more.

```java
package com.zetcode;

public class ShortCircuit {

    public static boolean One() {

        System.out.println("Inside one");
        return false;
    }

    public static boolean Two() {

        System.out.println("Inside two");
        return true;
    }

    public static void main(String[] args) {

        System.out.println("Short circuit");

        if (One() && Two()) {

            System.out.println("Pass");
        }

        System.out.println("#############");

        if (Two() || One()) {

            System.out.println("Pass");
        }
    }
}
```

We have two methods in the example. They are used as operands in boolean  
expressions. We will see if they are called.  

```java
if (One() && Two()) {

    System.out.println("Pass");
}
```


The `One` method returns `false`. The short circuit `&&` does not evaluate the  
second method. It is not necessary. Once an operand is `false`, the result of  
the logical conclusion is always `false`. Only "Inside one" is only printed to  
the console.  

```java
if (Two() || One()) {

    System.out.println("Pass");
}
```

In the second case, we use the `||` operator and use the Two method as the first  
operand. In this case, "Inside two" and "Pass" strings are printed to the  
terminal. It is again not necessary to evaluate the second operand, since once  
the first operand evaluates to true, the logical or is always true.  


## Relational operators

Relational operators are used to compare values. These operators always result  
in a boolean value.  

Here is the data you provided in a markdown table format:

| Symbol | Meaning               |
|--------|-----------------------|
| <      | less than             |
| <=     | less than or equal to |
| >      | greater than          |
| >=     | greater than or equal to |
| ==     | equal to              |
| !=     | not equal to          |


Relational operators are also called comparison operators.  

```java
void main() {

    System.out.println(3 < 4);
    System.out.println(3 == 4);
    System.out.println(4 >= 3);
    System.out.println(4 != 3);
}
```

In the code example, we have four expressions. These expressions compare integer  
values. The result of each of the expressions is either `true` or `false`. In  
Java we use the `==` to compare numbers. (Some languages like Ada, Visual Basic,  
or Pascal use `=` for comparing numbers.)  

## Bitwise operators

Decimal numbers are natural to humans. Binary numbers are native to computers.  
Binary, octal, decimal, or hexadecimal symbols are only notations of a number.  
Bitwise operators work with bits of a binary number. Bitwise operators are  
seldom used in higher level languages like Java.  

Here is the data you provided in a markdown table format:

| Symbol | Meaning             |
|--------|---------------------|
| ~      | bitwise negation    |
| ^      | bitwise exclusive or|
| &      | bitwise and         |
| \|     | bitwise or          |


The bitwise negation operator changes each 1 to 0 and 0 to 1.

```java
System.out.println(~7); // prints -8
System.out.println(~ -8); // prints 7
```

The operator reverts all bits of a number 7. One of the bits also determines  
whether the number is negative or not. If we negate all the bits one more time,  
we get number 7 again.  

The bitwise and operator performs bit-by-bit comparison between two numbers. The  
result for a bit position is 1 only if both corresponding bits in the operands  
are 1.

```
      00110
   &  00011
   =  00010
```

The first number is a binary notation of 6, the second is 3 and the result is 2.  

```java
System.out.println(6 & 3); // prints 2
System.out.println(3 & 6); // prints 2
```

The bitwise or operator performs bit-by-bit comparison between two numbers. The  
result for a bit position is 1 if either of the corresponding bits in the  
operands is 1.  

```
     00110
   | 00011
   = 00111
```

The result is `00110` or decimal 7.

```java
System.out.println(6 | 3); // prints 7
System.out.println(3 | 6); // prints 7
```

The bitwise exclusive or operator performs bit-by-bit comparison between two  
numbers. The result for a bit position is 1 if one or the other (but not both)  
of the corresponding bits in the operands is 1.  

```
      00110
   ^  00011
   =  00101
```

The result is `00101` or decimal 5.

```java
System.out.println(6 ^ 3); // prints 5
System.out.println(3 ^ 6); // prints 5
```

## Compound assignment operators

Compound assignment operators are shorthand operators which consist of two  
operators.

```java
a = a + 3;
a += 3;
```

The `+=` compound operator is one of these shorthand operators. The above two  
expressions are equal. Value 3 is added to the a variable.  

Other compound operators are:

```
-=   *=   /=   %=   &=   |=   <<=   >>=
```

The following example uses two compound operators.

```java
void main() {

    int a = 1;
    a = a + 1;

    System.out.println(a);

    a += 5;
    System.out.println(a);

    a *= 3;
    System.out.println(a);
}
```

We use the `+=` and `*=` compound operators.  

```java
int a = 1;
a = a + 1;
```

The `a` variable is initiated to one. Value 1 is added to the variable using the  
non-shorthand notation.  

```java
a += 5;
```

Using a `+=` compound operator, we add 5 to the a variable. The statement is  
equal to `a = a + 5;`.  

```java
a *= 3;
```

Using the `*=` operator, the a is multiplied by 3. The statement is equal to  
`a = a * 3;`.


## The instanceof operator

The `instanceof` operator compares an object to a specified type.  
 
```java
package com.zetcode;

class Base {}
class Derived extends Base {}

public class InstanceofOperator {

    public static void main(String[] args) {

        Base b = new Base();
        Derived d = new Derived();

        System.out.println(d instanceof Base);
        System.out.println(b instanceof Derived);
        System.out.println(d instanceof Object);
    }
}
```

In the example, we have two classes: one base and one derived from the base.  

```java
System.out.println(d instanceof Base);
```

This line checks if the variable d points to the class that is an instance of  
the `Base` class. Since the `Derived` class inherits from the `Base` class, it  
is also an instance of the Base class too. The line prints `true`.  

```java
System.out.println(b instanceof Derived);
```

The `b` object is not an instance of the `Derived` class. This line prints `false`.

```java
System.out.println(d instanceof Object);
```

Every class has Object as a superclass. Therefore, the `d` object is also an
instance of the `Object` class.

## The lambda operator

Lambda expressions allow to create more concise code in Java.  

```
(parameters) -> expression
(parameters) -> { statements; }
```

This is the basic syntax for a lambda expression in Java.  

The declaration of the type of the parameter is optional; the compiler can infer  
the type from the value of the parameter. For a single parameter the parentheses  
are optional; for multiple parameters, they are required.  

The curly braces are optional if there is only one statement in an expression  
body. Finally, the return keyword is optional if the body has a single  
expression to return a value; curly braces are required to indicate that the  
expression returns a value.  

```java
import java.util.Arrays;

void main() {

    String[] words = { "kind", "massive", "atom", "car", "blue" };

    Arrays.sort(words, (String s1, String s2) -> (s1.compareTo(s2)));

    System.out.println(Arrays.toString(words));
}
```

In the example, we define an array of strings. The array is sorted using the  
`Arrays.sort` method and a lambda expression.  

Lambda expressions are used primarily to define an inline implementation of a  
functional interface, i.e., an interface with a single method only. Interfaces  
are abstract types that are used to enforce a contract.  

```java
package com.zetcode;

interface GreetingService {

    void greet(String message);
}

public class LambdaExpression2 {

    public static void main(String[] args) {

        GreetingService gs = (String msg) -> {
            System.out.println(msg);
        };

        gs.greet("Good night");
        gs.greet("Hello there");
    }
}
```

In the example, we create a greeting service with the help of a lambda  
expression.  

```java
interface GreetingService {

    void greet(String message);
}
```

Interface `GreetingService` is created. All objects implementing this interface
must implement the greet method.

```java
GreetingService gs = (String msg) -> {
    System.out.println(msg);
};
```

We create an object that implements `GreetingService` with a lambda expression.
The object has a method that prints a message to the console.

```java
gs.greet("Good night");
```

We call the object's `greet` method, which prints a give message to the console.

There are some common functional interfaces, such as `Function`, `Consumer`, or
`Supplier`.

```java
import java.util.function.Function;

void main() {

    Function<Integer, Integer> square = (Integer x) -> x * x;
    System.out.println(square.apply(5));
}
```

The example uses a lambda expression to compute squares of integers.

```java
Function<Integer, Integer> square = (Integer x) -> x * x;
System.out.println(square.apply(5));
```

Function is a function that accepts one argument and produces a result. The  
operation of the lamda expression produces a square of the given integer.  


## The double colon operator

The double colon operator `::` is used to create a reference to a method.  

```java
package com.zetcode;

import java.util.function.Consumer;

public class DoubleColonOperator {

    private static void greet(String msg) {

        System.out.println(msg);
    }

    public static void main(String[] args) {

        Consumer<String> f = DoubleColonOperator::greet;
        f.accept("Hello there");
    }
}
```

In the code example, we create a reference to a static method with the double  
colon operator.  

```java
private static void greet(String msg) {

    System.out.println(msg);
}
```

We have a static method that prints a greeting to the console.  

```java
Consumer<String> f = DoubleColonOperator::greet;
```

`Consumer` is a functional interface that represents an operation that accepts a  
single input argument and returns no result. With the double colon operator, we  
create a reference to the greet method.  

```java
f.accept("Hello there");
```

We perform the functional operation with the accept method.

## Operator precedence

The operator precedence tells us which operators are evaluated first. The  
precedence level is necessary to avoid ambiguity in expressions.  

What is the outcome of the following expression, 28 or 40?

```
3 + 5 * 5
```

Like in mathematics, the multiplication operator has a higher precedence than  
addition operator. So the outcome is 28.  

```java
(3 + 5) * 5
```

To change the order of evaluation, we can use parentheses. Expressions inside  
parentheses are always evaluated first. The result of the above expression is  
40.


## Operators precedence list

The following table shows common Java operators ordered by precedence   
(highest precedence first):  

Here is the data you provided in a markdown table format:  

| Operator | Meaning | Associativity |
| --- | --- | --- |
| [] () . | array access, method invoke, object member access | Left-to-right |
| ++ -- + - | increment, decrement, unary plus and minus | Right-to-left |
| ! ~ (type) new | negation, bitwise NOT, type cast, object creation | Right-to-left |
| * / % | multiplication, division, modulo | Left-to-right |
| + - | addition, subtraction | Left-to-right |
| + | string concatenation | Left-to-right |
| << >> >>> | shift | Left-to-right |
| < <= > >= | relational | Left-to-right |
| instanceof | type comparison | Left-to-right |
| == != | equality | Left-to-right |
| & | bitwise AND | Left-to-right |
| ^ | bitwise XOR | Left-to-right |
| \| | bitwise OR | Left-to-right |
| && | logical AND | Left-to-right |
| \|\| | logical OR | Left-to-right |
| ? : | ternary | Right-to-left |
| = | simple assignment | Right-to-left |
| += -= *= /= %= &= | compound assignment | Right-to-left |
| ^= \|= <<= >>= >>>= | compound assignment | Right-to-left |

Table: Operator precedence and associativity  

Operators on the same row of the table have the same precedence. If we use  
operators with the same precedence, then the associativity rule is applied.  
 
```java
void main() {

    System.out.println(3 + 5 * 5);
    System.out.println((3 + 5) * 5);

    System.out.println(! true | true);
    System.out.println(! (true | true));
}
```

In this code example, we show a few expressions. The outcome of each expression  
is dependent on the precedence level.  

```java
System.out.println(3 + 5 * 5);
```

This line prints 28. The multiplication operator has a higher precedence than  
addition. First, the product of `5 * 5` is calculated, then 3 is added.  

```java
System.out.println(! true | true);
```

In this case, the negation operator has a higher precedence than the bitwise OR.  
First, the initial true value is negated to `false`, then the | operator combines  
`false` and `true`, which gives true in the end.  

## Associativity rule

Sometimes the precedence is not satisfactory to determine the outcome of an  
expression. There is another rule called associativity. The associativity of  
operators determines the order of evaluation of operators with the same  
precedence level.  

```
9 / 3 * 3
```

What is the outcome of this expression, 9 or 1? The multiplication, deletion,  
and the modulo operator are left to right associated. So the expression is  
evaluated this way: (9 / 3) * 3 and the result is 9.  


Arithmetic, boolean, relational, and bitwise operators are all left to right  
associated. The assignment operators, ternary operator, increment, decrement,  
unary plus and minus, negation, bitwise NOT, type cast, object creation  
operators are right to left associated.  

```java
void main() {

    int a, b, c, d;
    a = b = c = d = 0;

    String str = String.format("%d %d %d %d", a, b, c, d);
    System.out.println(str);

    int j = 0;
    j *= 3 + 1;
    System.out.println(j);
}
```

In the example, we have two cases where the associativity rule determines the  
expression.  

```java
int a, b, c, d;
a = b = c = d = 0;
```

The assignment operator is right to left associated. If the associativity was  
left to right, the previous expression would not be possible.  

```java
int j = 0;
j *= 3 + 1;
```

The compound assignment operators are right to left associated. We might expect  
the result to be 1. But the actual result is 0. Because of the associativity.  
The expression on the right is evaluated first and then the compound assignment  
operator is applied.  

## Ternary operator

The ternary operator `?:` is a conditional operator. It is a convenient operator  
for cases where we want to pick up one of two values, depending on the  
conditional expression.

```
cond-exp ? exp1 : exp2
```

If cond-exp is `true`, exp1 is evaluated and the result is returned. If the
cond-exp is `false`, exp2 is evaluated and its result is returned.

```java
void main() {

    int age = 31;

    boolean adult = age >= 18 ? true : false;

    System.out.println(String.format("Adult: %s", adult));
}
```

In most countries the adulthood is based on the age. You are adult if you are  
older than a certain age. This is a situation for a ternary operator.  

```java
boolean adult = age >= 18 ? true : false;
```

First the expression on the right side of the assignment operator is evaluated.  
The first phase of the ternary operator is the condition expression evaluation.  
So if the age is greater or equal to 18, the value following the ? character is  
returned. If not, the value following the : character is returned. The returned  
value is then assigned to the adult variable.  


## Calculating prime numbers

In the following example, we are going to calculate prime numbers.

```java

void main() {

    int[] nums = {0, 1, 2, 3, 4, 5, 6, 7, 8,
            9, 10, 11, 12, 13, 14, 15, 16, 17, 18,
            19, 20, 21, 22, 23, 24, 25, 26, 27, 28};

    System.out.print("Prime numbers: ");

    for (int num : nums) {

        if (num == 0 || num == 1) {
            continue;
        }

        if (num == 2 || num == 3) {

            System.out.print(num + " ");
            continue;
        }

        int i = (int) Math.sqrt(num);

        boolean isPrime = true;

        while (i > 1) {

            if (num % i == 0) {

                isPrime = false;
            }

            i--;
        }

        if (isPrime) {

            System.out.print(num + " ");
        }
    }

    System.out.print('\n');
}
```
 
In the above example, we deal with several operators. A prime number (or a  
prime) is a natural number that has exactly two distinct natural number  
divisors: 1 and itself. We pick up a number and divide it by numbers from 1 to  
the selected number. Actually, we do not have to try all smaller numbers; we can  
divide by numbers up to the square root of the chosen number. The formula will  
work. We use the remainder division operator.  

```java
int[] nums = { 0, 1, 2, 3, 4, 5, 6, 7, 8,
    9, 10, 11, 12, 13, 14, 15, 16, 17, 18,
    19, 20, 21, 22, 23, 24, 25, 26, 27, 28 };
```

We will calculate primes from these numbers.

```java
if (num == 0 || num == 1) {
    continue;
}
```

Values 0 and 1 are not considered to be primes.

```java
if (num == 2 || num == 3) {

    System.out.print(num + " ");
    continue;
}
```

We skip the calculations for 2 and 3. They are primes. Note the usage of the  
equality and conditional or operators. The `==` has a higher precedence than the  
`||` operator. So we do not need to use parentheses.  

```java
int i = (int) Math.sqrt(num);
```

We are OK if we only try numbers smaller than the square root of a number in
question.

```java
while (i > 1) {
    ...
    i--;
}
```

This is a while loop. The i is the calculated square root of the number. We use  
the decrement operator to decrease i by one each loop cycle. When i is smaller  
than 1, we terminate the loop. For example, we have number 9. The square root of  
9 is 3. We will divide the 9 number by 3 and 2. This is sufficient for our  
calculation.

```java
if (num % i == 0) {

    isPrime = false;
}
```

If the remainder division operator returns 0 for any of the `i` values, then the  
number in question is not a prime.  
