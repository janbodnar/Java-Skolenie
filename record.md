# Java record


A record is a type that is designed to hold immutable data. It is very useful  
for data analysis. The record type simplifies code and improves its readability.  
It removes unnecessary boilerplate.  

```java
record User(String name, String occupation) {
}
```

This is a definition of a simple record. The compiler automatically creates two  
final fields and two public read accessors. A public constructor is derived from  
the record parameters.  

The compiler auto-generates `hashCode`, `equals`, and `toString` methods.

Java record cannot extend any class, cannot declare instance fields, and cannot  
be abstract. A record can implement interfaces. We can also define our own  
constructors and methods.  

Other languages also have similar types. C# and F# have records, Scala case  
classes, and Kotlin data classes.  
 
# Example
The following is a simple example with a Java record.

```java
void main() {

    var u = new User("John Doe", "gardener");
    System.out.println(u);

    System.out.println(u.name());
    System.out.println(u.occupation());
}

record User(String name, String occupation) {
}
```

The program defines a `User` record with two string parameters.

```java
record User(String name, String occupation) {
}
```

The definition of a Java record is concise.

```java
var u = new User("John Doe", "gardener");
```

A new instance of a record is created with the `new` keyword.

```java
System.out.println(u);
```

We pass the record instance to the `System.out.println`, invoking record's  
`toString` method.  

```java
System.out.println(u.name());
System.out.println(u.occupation());
```

We call the two auto-generated getters.


## Comparing records

Java record auto-generates the equals method. It provides a value-based  
equality.

```java
void main() {

    var u = new User("John Doe", "gardener");
    var u2 = new User("Roger Roe", "driver");
    var u3 = new User("John Doe", "gardener");

    if (u.equals(u2)) {
        System.out.println("users are equal");
    } else {
        System.out.println("users are not equal");
    }

    if (u.equals(u3)) {
        System.out.println("users are equal");
    } else {
        System.out.println("users are not equal");
    }
}

record User(String name, String occupation) {
}
```

The program compares three User record types.


## Sorting records

The next example sorts records.

```java
import java.util.Comparator;
import java.util.List;

void main() {

    var users = List.of(
            new User("John", "Doe", 1230),
            new User("Lucy", "Novak", 670),
            new User("Ben", "Walter", 2050),
            new User("Robin", "Brown", 2300),
            new User("Amy", "Doe", 1250),
            new User("Joe", "Draker", 1190),
            new User("Janet", "Doe", 980),
            new User("Albert", "Novak", 1930));

    var sorted = users.stream().sorted(Comparator.comparingInt(User::salary)).toList();
    System.out.println(sorted);
}

record User(String fname, String lname, int salary) {
}
```

We have a `User` record with three arguments; we sort the users by their  
salaries.

```java
var sorted = users.stream().sorted(Comparator.comparingInt(User::salary)).toList();
```

We use Java stream to sort the data.

## Customize record

We can customize record types by overriding methods or defining custom ones.

```java
import java.util.List;

void main() {

    var users = List.of(
            new User("John", "Doe", 1230),
            new User("Lucy", "Novak", 670),
            new User("Ben", "Walter", 2050),
            new User("Robin", "Brown", 2300),
            new User("Amy", "Doe", 1250),
            new User("Joe", "Draker", 1190),
            new User("Janet", "Doe", 980),
            new User("Albert", "Novak", 1930));

    var sorted = users.stream().sorted().toList();
    System.out.println(sorted);
}

record User(String fname, String lname, int salary) implements Comparable<User> {
    @Override
    public int compareTo(User u) {
        return this.lname.compareTo(u.lname);
    }
}
```

The program defines a custom comparator. The default comparison of the `User`  
type is by last name.  

```java
record User(String fname, String lname, int salary) implements Comparable<User> {
    @Override
    public int compareTo(User u) {
        return this.lname.compareTo(u.lname);
    }
}
```

The record implements the `Comparable` interface and overrides the `compareTo`  
method where we compare the users' last names.  

## Filtering records

The next example filters a list of records.

```java
import java.util.List;
import java.util.stream.Collectors;

void main() {

    var users = List.of(
            User.of("John", "Doe", 1230),
            User.of("Lucy", "Novak", 670),
            User.of("Ben", "Walter", 2050),
            User.of("Robin", "Brown", 2300),
            User.of("Amy", "Doe", 1250),
            User.of("Joe", "Draker", 1190),
            User.of("Janet", "Doe", 980),
            User.of("Albert", "Novak", 1930));

    var filtered = users.stream().filter(e -> e.salary() > 2000)
            .collect(Collectors.toList());
    System.out.println(filtered);
}

record User(String fname, String lname, int salary) {
    public static User of(String fname, String lname, int salary) {
        return new User(fname, lname, salary);
    }
}
```

We have a list of User records. We filter the users by their salary.  

```java
var filtered = users.stream().filter(e -> e.salary() > 2000)
        .collect(Collectors.toList());
```

We filter out all users whose salary is bigger than 2000.
