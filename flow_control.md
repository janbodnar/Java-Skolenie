# Control flow statements

In Java language there are several keywords that are used to alter the flow of  
the program. Statements can be executed multiple times or only under a specific  
condition. The if, else, and switch statements are used for testing conditions,  
the while and for statements to create cycles, and the break and continue  
statements to alter a loop.  


When the program is run, the statements are executed from the top of the source  
file to the bottom. One by one.  


## The if statement

The if statement has the following general form:

```java
if (expression) {

    statement;
}
```

The `if` keyword is used to check if an expression is true. If it is true, a  
statement is then executed. The statement can be a single statement or a  
compound statement. A compound statement consists of multiple statements  
enclosed by a block. A block is code enclosed by curly brackets. The brackets  
are optional if we have only one statement in the body.  

```java
import java.util.Random;

void main() {

    var r = new Random();
    int num = r.nextInt();

    if (num > 0) {

        System.out.println("The number is positive");
    }
}
```

A random number is generated. If the number is greater than zero, we print a
message to the terminal.

```java
var r = new Random();
int num = r.nextInt();
```

These two lines generate a random integer. The number can be positive or
negative.

```java
if (num > 0) {

    System.out.println("The number is positive");
}
```

Using the `if` keyword, we check if the generated number is greater than zero.  
The if keyword is followed by a pair of round brackets. Inside the brackets, we  
place an expression. The expression results in a boolean value. If the boolean  
value is true, then the block enclosed by two curly brackets is executed. In our  
case, the string "The number is positive" is printed to the terminal. If the  
random value is negative, nothing is done. The curly brackets are optional if we  
have only one expression.  

## The else keyword

We can use the else keyword to create a simple branch. If the expression inside  
the square brackets following the if keyword evaluates to false, the statement  
following the else keyword is automatically executed.  

```java
import java.util.Random;

void main() {

    var r = new Random();
    int num = r.nextInt();

    if (num > 0) {

        System.out.println("The number is positive");

    } else {

        System.out.println("The number is negative");
    }
}
```

Either the block following the if keyword or the block following the else  
keyword is executed.

```java
if (num > 0) {

    System.out.println("The number is positive");

} else {

    System.out.println("The number is negative");
}
```

The `else` keyword follows the right curly bracket of the `if` block. It has its  
own block enclosed by a pair of curly brackets.

## Multiple branches with if else

We can create multiple branches using the `else if` keyword. The `else if`  
keyword tests for another condition if and only if the previous condition was  
not met. Note that we can use multiple `else if` keywords in our tests.   

The previous program had a slight issue. Zero was given to negative values. The   
following program will fix this.   

```java
import java.util.Scanner;

void main() {

    System.out.print("Enter an integer:");

    try (var sc = new Scanner(System.in)) {
        
        int num = sc.nextInt();

        if (num < 0) {

            System.out.println("The integer is negative");
        } else if (num == 0) {

            System.out.println("The integer equals to zero");
        } else {

            System.out.println("The integer is positive");
        }
    }
}
```

We receive a value from the user test it if it is a negative number or positive,  
or if it equals to zero.

```java
System.out.print("Enter an integer:");
```

A prompt to enter an integer is written to the standard output.

```java
Scanner sc = new Scanner(System.in);
int num = sc.nextInt();
```

Using the Scanner class of the `java.util` package, we read an integer value  
from the standard input.  

```java
if (num < 0) {

    System.out.println("The integer is negative");
} else if (num == 0) {

    System.out.println("The integer equals to zero");
} else {

    System.out.println("The integer is positive");
}
```

If the first condition evaluates to true, e.g. the entered value is less than   
zero, the first block is executed and the remaining two blocks are skipped. If  
the first condition is not met, then the second condition following the `if else`  
keywords is checked. If the second condition evaluates to true, the second block  
is executed. If not, the third block following the else keyword is executed. The  
else block is always executed if the previous conditions were not met.  


## The switch statement

The `switch` statement is a selection control flow statement. It allows the  
value of a variable or expression to control the flow of a program execution via  
a multi-way branch. It creates multiple branches in a simpler way than using the  
combination of if and else if statements. Each branch is ended with the break  
keyword.  

We use a variable or an expression. The `switch` keyword is used to test a value  
from the variable or the expression against a list of values. The list of values  
is presented with the `case` keyword. If the values match, the statement  
following the ca`se is executed. There is an optional default statement. It is  
executed if no other match is found.  

```java
import java.util.Scanner;

void main() {

    System.out.print("Enter a domain:");

    try (var sc = new Scanner(System.in)) {

        String domain = sc.nextLine();
        domain = domain.trim().toLowerCase();

        switch (domain) {

            case "us":
                System.out.println("United States");
                break;

            case "de":
                System.out.println("Germany");
                break;

            case "sk":
                System.out.println("Slovakia");
                break;

            case "hu":
                System.out.println("Hungary");
                break;

            default:
                System.out.println("Unknown");
                break;
        }
    }
}
```

The user is requested to enter a domain name. The domain name is read and stored  
in a variable. The variable is tested with the switch keyword against a list of  
options. In our program, we have a domain variable. We read a value for the  
variable from the command line. We use the case statement to test for the value  
of the variable. There are several options. If the value equals for example to  
"us", the "United States" string is printed to the console.  

```java
try (var sc = new Scanner(System.in)) {

    String domain = sc.nextLine();
```

The input from the user is read from the console.

```java
domain = domain.trim().toLowerCase();
```

The trim method strips the variable from potential leading and trailing white  
spaces. The toLowerCase converts the characters to lowercase. Now the "us",  
"US", or "us " are viable options for the us domain name.  

```java
switch (domain) {
    ...
}
```

In the round brackets, the `switch` keyword takes an input which is going to be  
tested. The input can be of `byte`, `short`, `char`, `int`, `enum`, or `String`  
data type. The body of the `switch` keyword is placed inside a pair or curly  
brackets. Inside the body, we can place multiple `case` options. Each option is  
ended with the `break` keyword.

```java
case "us":
    System.out.println("United States");
    break;
```

In this case option, we test if the domain variable is equal to "us" string. If  
true, we print a message to the console. The option is ended with the `break`  
keyword. If one of the options is successfully evaluated, the break keyword  
terminates the `switch` block.  

```java
default:
    System.out.println("Unknown");
    break;
```

The default keyword is optional. If none of the case options is evaluated, then  
the default section is executed.  


## The switch expression

Java switch expression simplifies the original switch statement. It allows using  
multiple case labels called arms.

```java
import java.util.Scanner;

void main() {

    System.out.print("Enter a domain: ");

    try (var sc = new Scanner(System.in)) {

        String domain = sc.nextLine();
        domain = domain.trim().toLowerCase();

        switch (domain) {

            case "us" -> System.out.println("United States");
            case "de" -> System.out.println("Germany");
            case "sk" -> System.out.println("Slovakia");
            case "hu" -> System.out.println("Hungary");
            default -> System.out.println("Unknown");
        }
    }
}
```

The previous `switch` statement example is rewritten using switch expression.  

```java
case "us" -> System.out.println("United States");
```

The switch expression the `->` to separate label from the statement. The break  
statement is not needed, once an option is matched, other options are not  
evaluated.  

## Switch expressions can return values.

```java
import java.util.Scanner;

void main() {

    System.out.print("Enter a domain: ");

    try (var sc = new Scanner(System.in)) {

        String domain = sc.nextLine();
        domain = domain.trim().toLowerCase();

        String res = switch (domain) {

            case "us" -> "United States";
            case "de" -> "Germany";
            case "sk" -> "Slovakia";
            case "hu" -> "Hungary";
            default -> "Unknown";
        };

        System.out.println(res);
    }
}
```

This is a modified version of the previous example. The arms now return a string  
value, which is printed later.  

##  The while statement

The while statement is a control flow statement that allows code to be executed  
repeatedly based on a given boolean condition.  

```
while (expression) {

    statement;
}
```

The `while` keyword executes the statements inside the block enclosed by the  
curly brackets. The statements are executed each time the expression is  
evaluated to true.  

```java
void main() {

    int i = 0;
    int sum = 0;

    while (i < 10) {

        i++;
        sum += i;
    }

    System.out.println(sum);
}
```

In the code example, we calculate the sum of values from a range of numbers.  

The while loop has three parts: initialization, testing, and updating. Each  
execution of the statement is called a cycle.  

```java
int i = 0;
```

We initiate the i variable. It is used as a counter.

```java
while (i < 10) {
    ...
}
```

The expression inside the round brackets following the while keyword is the  
second phase, the testing. The statements in the body are executed until the  
expression is evaluated to false.  

```java
i++;
```

The last phase of the `while` loop is the updating. We increment the counter.  
Note that improper handling of the `while` loops may lead to endless cycles.  

There is a modified version of the while statement. It is the do while  
statement. It is guaranteed that the statements inside the block are run at  
least once, even if the condition is not met.  

```java
void main() {

    int count = 0;

    do {
        System.out.println(count);
    } while (count != 0);
}
```

First the block is executed and then the truth expression is evaluated. In our  
case, the condition is not met and the do while statement terminates.  

## The for statement

When the number of cycles is know before the loop is initiated, we can use the  
for statement. In this construct we declare a counter variable, which is  
automatically increased or decreased in value during each repetition of the  
loop.  

```java
void main() {

    for (int i = 0; i < 10; i++) {

        System.out.println(i);
    }
}
```

In this example, we print numbers 0..9 to the console.

```java
for (int i = 0; i < 10; i++) {

    System.out.println(i);
}
```

There are three phases in a for loop. First, we initiate the counter i to zero.  
This phase is done only once. Next comes the condition. If the condition is met,  
the statement inside the for block is executed. Then comes the third phase: the  
counter is increased. Now we repeat 2 and 3 phases until the condition is not  
met and the for loop is terminated. In our case, when the counter i is equal to  
10, the for loop stops executing.  

A for loop can be used for easy traversal of an array. From the length property  
of the array, we know the size of the array.  

```java
void main() {

    String[] planets = { "Mercury", "Venus", "Earth",
            "Mars", "Jupiter", "Saturn", "Uranus", "Pluto" };

    for (int i = 0; i < planets.length; i++) {

        System.out.println(planets[i]);
    }

    System.out.println("In reverse:");

    for (int i = planets.length - 1; i >= 0; i--) {

        System.out.println(planets[i]);
    }
}
```

We have an array holding the names of planets in our Solar System. Using two for  
loops, we print the values in ascending and descending orders.  

```java
for (int i = 0; i < planets.length; i++) {

    System.out.println(planets[i]);
}
```

The arrays are accessed by zero-based indexing. The first item has index 0.  
Therefore, the i variable is initialized to zero. The condition checks if the `i`  
variable is less than the length of the array. In the final phase, the `i`  
variable is incremented.  

```java
for (int i = planets.length - 1; i >= 0; i--) {

    System.out.println(planets[i]);
}
```

This for loop prints the elements of the array in reverse order. The `i` counter  
is initialized to array size. Since the indexing is zero based, the last element  
has index array `size-1`. The condition ensures that the counter is greater or  
equal to zero. (Array indexes cannot be negative). In the third step, the `i`  
counter is decremented by one.  

More expressions can be placed in the initialization and iteration phase of the  
for loop.

```java
import java.util.Arrays;
import java.util.Random;

void main() {

    var r = new Random();

    int[] values = new int[10];
    int num;
    int sum = 0;

    for (int i = 0; i < 10; i++, sum += num) {

        num = r.nextInt(10);
        values[i] = num;
    }

    System.out.println(Arrays.toString(values));
    System.out.println("The sum of the values is " + sum);
}
```

In our example, we create an array of ten random numbers. A sum of the numbers  
is calculated.

```java
for (int i = 0; i < 10; i++, sum += num) {

    num = r.nextInt(10);
    values[i] = num;
}
```

In the third part of the for loop, we have two expressions separated by a comma  
character. The i counter is incremented and the current number is added to the  
sum variable.  


## Enhanced for statement

The enhanced for statement simplifies traversing over collections of data. It  
has no explicit counter. The statement goes through an array or a collection one  
by one and the current value is copied to a variable defined in the construct.  

```java
void main() {

    String[] planets = {
            "Mercury", "Venus", "Earth",
            "Mars", "Jupiter", "Saturn", "Uranus", "Pluto"
    };

    for (String planet : planets) {

        System.out.println(planet);
    }
}
```

In this example, we use the enhanced for statement to go through an array of  
planets.

```java
for (String planet : planets) {

    System.out.println(planet);
}
```

The usage of the for statement is straightforward. The planets is the array that  
we iterate through. A `planet` is the temporary variable that has the current  
value from the array. The for statement goes through all the `planets` and  
prints them to the console.  


## The break statement

The `break` statement can be used to terminate a block defined by `while`,  
`for`, or `switch` statements.  

```java
import java.util.Random;

void main() {

    var random = new Random();

    while (true) {

        int num = random.nextInt(30);
        System.out.print(num + " ");

        if (num == 22) {

            break;
        }
    }

    System.out.print('\n');
}
```

We define an endless while loop. We use the break statement to get out of this  
loop. We choose a random value from 1 to 30 and print it. If the value equals to  
22, we finish the endless while loop.  

```java
while (true) {
    ...
}
```

Placing `true` in the brackets of the while statement creates an endless loop.  
We must terminate the loop ourselves. Note that such code is error-prone. We  
should be careful using such loops.  

```java
if (num == 22) {

    break;
}
```

When the randomly chosen value is equal to 22, the `break` statement is executed  
and the while loop is terminated.


## The continue statement

The `continue` statement is used to skip a part of the loop and continue with  
the next iteration of the loop. It can be used in combination with for and `while`  
statements.  

In the following example, we print a list of numbers that cannot be divided by 2  
without a remainder.

```java
void main() {

    int num = 0;

    while (num < 100) {

        num++;

        if (num % 2 == 0) {
            continue;
        }

        System.out.print(num + " ");
    }

    System.out.print('\n');
}
```

We iterate through numbers 1..99 with the while loop.

```java
if (num % 2 == 0) {
    continue;
}
```

If the expression `num % 2` returns 0, the number in question can be divided by  
2. The `continue` statement is executed and the rest of the cycle is skipped. In  
our case, the last statement of the loop is skipped and the number is not  
printed to the console. The next iteration is started.  
