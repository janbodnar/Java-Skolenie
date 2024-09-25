# Switch expressions

Switch expressions offer a more concise and readable way to write multi-way  
branching logic. They are a powerful enhancement for the classic switch  
statements.  

Unlike traditional switch statements, the switch expressions can return values.

Java switch expressions support using multiple case labels. These are also  
called arms. Each case label is followed by the `->` arrow syntax.  

The switch expressions must be exhaustive. With the exception of few cases such  
as enumerations, where the compiler can determine all possible options, we must  
use the default arm. It is executed when no other option matches.  

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

The user is requested to enter a domain name. The domain name is read and stored  
in a variable. The variable is tested with the `switch` keyword against a list  
of options. In our program, we have a domain variable. We read a value for the  
variable from the command line.  

```java
case "us" -> System.out.println("United States");
```

We use the case statement to test for the value of the variable. There are  
several options. If, for instance, the value equals to "us", the "United States"  
string is printed to the console. Once an option matches, no other arms are  
evaluated.  

```java
default -> System.out.println("Unknown");
```

The default branch is executed when the value does not match any previous  
branch.  

## Using primitive types

`boolean` values:  

```java
import java.util.Random;

void main() {

    boolean isGirl = new Random().nextBoolean();

    String name = pickName(isGirl);
    System.out.printf("chosen name: %s %n", name);
}

String pickName(boolean isGirl) {

    return switch (isGirl) {
        case true -> "Zuzana";
        case false -> "Martin";
    };
}
```

int values: 

```java
import java.util.Arrays;

void main() {

    int[] ages = { 12, 23, 45, 0, 67, 88, 43, 55, -4};

    Arrays.stream(ages).forEach(e -> System.out.println(e + ": " + checkAge(e)));
}

String checkAge(int age) {

    return switch (age) {
        case int i when i < 18 && i > 0-> "minor";
        case int i when i >= 18 && i < 64 -> "adult";
        case int i when i > 64 -> "senior";
        default -> "n/a";
    };
}
```


## Using enumerations

In the next example, we work with enumerations.

```java
import java.util.Random;

void main() {

    Season season = Season.randomSeason();

    String msg = switch (season) {

        case Season.SPRING -> "Spring";
        case Season.SUMMER -> "Summer";
        case Season.AUTUMN -> "Autumn";
        case Season.WINTER -> "Winter";
    };

    System.out.println(msg);
}

enum Season {
    SPRING,
    SUMMER,
    AUTUMN,
    WINTER;

    public static Season randomSeason() {
        
        var random = new Random();
        int ridx = random.nextInt(Season.values().length);
        return Season.values()[ridx];
    }
}
```

We define a `Season` enumeration. The enumeration contains a `randomSeason`  
method which creates a `Season` value randomly. Depending on the chosen value,  
we print a message.  

```java
var msg = switch (season) {

    case Season.Spring -> "Spring";
    case Season.Summer -> "Summer";
    case Season.Autumn -> "Autumn";
    case Season.Winter -> "Winter";
};

System.out.println(msg);
```

We check the value against the switch expression. The expression returns the  
string representation of the enum. Note that the switch expression is  
exhaustive.  

## Checking multiple options

We can check multiple options in one branch.  

```java
import java.util.Random;

void main() {

    Grade grade = Grade.randomGrade();

    String msg = switch (grade) {

        case Grade.A, Grade.B, Grade.C, Grade.D, Grade.E, Grade.F -> "passsed";
        case Grade.FX -> "failed";
    };

    System.out.println(STR."\{grade} - \{msg}");
}

enum Grade {
    A, B, C, D, E, F, FX;

    public static Grade randomGrade() {

        var random = new Random();
        int rdx = random.nextInt(Grade.values().length);
        return Grade.values()[rdx];
    }
}
```

We have a list of grades. For A throug F grades, we pass the example. For the FX   
grade, we fail the exam.  

```java
String msg = switch (grade) {

    case Grade.A, Grade.B, Grade.C, Grade.D, Grade.E, Grade.F -> "passsed";
    case Grade.FX -> "failed";
};
```

We check six options in the first branch. They are separated with a comma.

## Checking types

In the following program, we check the types of values.

```java
import java.math.BigDecimal;
import java.util.List;

void main() {

    List<Object> objects = List.of("falcon", new BigDecimal(120001212),
            new int[] { 1, 2, 3, 4, 5 }, new String[] { "sky", "blue", "rock" });

    objects.forEach(e -> System.out.println(checkType(e)));
}

String checkType(Object o) {

    return switch (o) {
        case String str -> "String";
        case BigDecimal bd -> "BigDecimal";
        case Integer i -> "Integer";
        case int[] ai -> "Array of integers";
        case String[] as -> "Array of strings";
        default -> "n/a";
    };
}
```

We have a list of objects of various types. Using switch expression, we  
determine the type of each value.  

```java
return switch (o) {
    case String str -> "String";
    case BigDecimal bd -> "BigDecimal";
    case Integer i -> "Integer";
    case int[] ai -> "Array of integers";
    case String[] as -> "Array of strings";
    default -> "n/a";
};
```

After the case keyword, we provide the type. If the type matches, the arm is  
executed and the corresponding string is returned.  

## When guards
 
When guards can be used to apply simple expressions on options. The expressions  
can be compined with `&&` and `||` operators.  

```java
import java.util.Arrays;

void main() {

    int[] ages = { 12, 23, 45, 0, 67, 88, 43, 55, -4};

    Arrays.stream(ages).forEach(e -> System.out.println(STR."\{e} - \{checkAge(e)}"));
}

String checkAge(Integer age) {

    return switch (age) {
        case Integer i when i < 18 && i > 0-> "minor";
        case Integer i when i >= 18 && i < 64 -> "adult";
        case Integer i when i > 64 -> "senior";
        default -> "n/a";
    };
}
```

We have an array of integers representing ages. We use the switch expression to  
map the values into age categories.  

```java
return switch (age) {
    case Integer i when i < 18 && i > 0-> "minor";
    case Integer i when i >= 18 && i < 64 -> "adult";
    case Integer i when i > 64 -> "senior";
    default -> "n/a";
};
```

After the when keyword, we use the < 18 && i > 0-> expression to check if the  
number falls between 0 and 18.  

## Null values

It is possible to check for nulls in switch expressions.

```java
import java.util.List;
import java.util.ArrayList;

void main() {

    List<Integer> data = new ArrayList<>();
    data.add(2);
    data.add(5);
    data.add(0);
    data.add(null);
    data.add(-4);
    data.add(6);

    data.forEach(e -> System.out.println(STR."\{e} - \{checkValue(e)}"));
}

String checkValue(Integer i) {

    return switch (i) {
        case null -> "null value";
        case 0 -> "zero value";
        case Integer n when n > 0 -> "positive value";
        case Integer n when n < 0 -> "negative value";
        default -> "n/a";
    };
};
```

We have a list of integers; there is also one null value.

```java
case null -> "null value";
```

This arm checks if the value is null.

## Record fields

It is possible to check record fields in when guards.

```java
import java.util.List;

void main() {

    var points = List.of(Point.of(0, 0), Point.of(-3, -3), Point.of(-3, -3),
            Point.of(12, -1));

    points.forEach(p -> System.out.println(STR."\{p} - \{checkQuadrant(p)}"));
}

String checkQuadrant(Point p) {

    return switch (p) {
        case Point(var x, var y) when x == 0 && y == 0 -> "origin";
        case Point(var x, var y) when x > 0 && y > 0 -> "Q I";
        case Point(var x, var y) when x < 0 && y > 0 -> "Q II";
        case Point(var x, var y) when x < 0 && y < 0 -> "Q III";
        case Point(var x, var y) when x > 0 && y < 0 -> "Q IV";
        default -> "n/a";
    };
};

record Point(int x, int y) {
    static Point of(int x, int y) {
        return new Point(x, y);
    }
}
```

We have a list of points of a coordinate system. We map each point to its  
corresponding quadrant.  

```java
return switch (p) {
    case Point(var x, var y) when x == 0 && y == 0 -> "origin";
    case Point(var x, var y) when x > 0 && y > 0 -> "Q I";
    case Point(var x, var y) when x < 0 && y > 0 -> "Q II";
    case Point(var x, var y) when x < 0 && y < 0 -> "Q III";
    case Point(var x, var y) when x > 0 && y < 0 -> "Q IV";
    default -> "n/a";
};
```

The record follows the case keyword. After the when guard, we can work with the  
fields in expression directly.  
