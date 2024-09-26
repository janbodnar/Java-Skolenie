# enum

The `enum` type is built-in Java data type that defines a fixed set of named  
constants. The set of constants cannot be changed afterwards. Variables having  
an enum type can be assigned any of the enumerators as a value.  

The enum type provides a more robust and readable way to handle constant values  
compared to using primitive data types like integers. Enemerations enforce type  
safety by guaranteeing that the variable can only hold one of the predefined  
values.  

We should use enum types any time we need to represent a fixed set of constants.  
There are many natural enum types such as the planets in our solar system,  
seasons, or days of week. These are data sets where we know all possible values  
at compile time.  

```java
public enum Size {
    SMALL, MEDIUM, LARGE
}
```

We use the `enum` keyword to define an enumeration in Java. It is a good  
programming practice to name the constants with uppercase letters.  

## Example

We have a simple code example with an enumeration.

```java
enum Day {

    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY,
    SUNDAY
}

void main() {

    Day day = Day.MONDAY;

    if (day == Day.MONDAY) {

        System.out.println("It is Monday");
    }

    System.out.println(day);

    for (Day d : Day.values()) {

        System.out.println(d);
    }
}
```

We define the `Day` enum that represents a fixed set of seven day names.

```java
enum Day {

    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY,
    SUNDAY
}
```

An enum type is created with the `enum` keyword. By convention, constants are  
written in uppercase letters.  

```java
Day day = Day.MONDAY;
```

We have a variable called day which is of enumerated type `Day`. It is
initialized to `Day.Monday`.  

```java
for (Day d : Day.values()) {

    System.out.println(d);
}
```

This loop prints all days to the console. The values method returns an array  
containing the constants of this enum type, in the order they are declared. This  
method may be used to iterate over the constants with the enhanced for  
statement. The enhanced for goes through the array, element by element, and  
prints them to the terminal.  


## Providing values to enum constants

We can explicitly provide some values to the enumeration constants.

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

        System.out.println(STR."\{season} \{season.getValue()}");
    }
}
```

The example contains a `Season` enumeration which has four constants.

```java
SPRING(10),
SUMMER(20),
AUTUMN(30),
WINTER(40);
```

Here we define four constants of the enum. The constants are given specific  
values.  


## Toss a coin

Enumeration is a type of a class. We can define our own methods.

```java
import java.util.Random;

enum Coin {
    HEADS,
    TAILS;

    public static Coin toss() {

        var rand = new Random();
        int rdx = rand.nextInt(Coin.values().length);
        return Coin.values()[rdx];
    }
}

void main() {

    for (int i = 1; i <= 15; i++) {

        System.out.printf("%s ", Coin.toss());
    }
}
```

The example defines the toss method, which randomly chooses one of the
constants: HEADS or TAILS. Later in the for loop we call toss fifteen times.

## Enum type with switch expressions

Enums can be effectively used with switch expressions.

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
method which creates a Season value randomly. Depending on the chosen value, we  
print a message.  

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
string representation of the enum. Since the compiler knows all the possible  
constants beforehand, the switch expression is exhaustive, that is, we do not  
have to define the default arm.  

## Modify example

Add `MaritalStatus` enum to the example and filter all single users.  

```java
import java.util.List;

void main() {

    List<User> users = List.of(
            new User("Jack", "jack234@gmail.com"),
            new User("Peter", "pete2@post.com"),
            new User("Lucy", "lucy17@gmail.com"),
            new User("Robert", "bob56@post.com"),
            new User("Martin", "mato4@imail.com")
    );

    List<User> res = users.stream()
            .filter(user -> user.email().matches(".*post.com"))
            .toList();

    res.forEach(p -> System.out.println(p.name()));
}

record User(String name, String email) {
}
```
