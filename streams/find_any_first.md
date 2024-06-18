# findFirst & findAny


The `findFirst` method returns an `Optional` describing the first element of a  
stream, or an empty `Optional` if the stream is empty.  

The `findAny` method returns an `Optional` describing some element of a stream,  
or an empty `Optional` if the stream is empty.  

# The findFirst example

In the next example we use the `findFirst` method.

```java
import java.util.List;

void main() {

    var words = List.of("war", "cup", "cloud", "alert", "be", "ocean", "book");
    var empty = List.of();

    var first = words.stream().findFirst().orElse("not found");
    System.out.println(first);

    var first2 = empty.stream().findFirst().orElse("not found");
    System.out.println(first2);
}
```

We find first elements of the list of words.  

```java
var words = List.of("war", "cup", "cloud", "alert", "be", "ocean", "book");
var empty = List.of();
```

We have two lists of strings. One has seven words, the other is empty.  

```java
var first = words.stream().findFirst().orElse("not found");
```

We find the first element of the list. If no element is found, we return  
"not found" string.  


In the second example, we filter a list of words and then find its first  
matching element.

```java
import java.util.List;

void main() {

    var words = List.of("war", "cup", "cloud", "alert", "be",
            "water", "warm", "ocean", "book");

    var first = words.stream().filter(e -> e.startsWith("w"))
            .findFirst().orElse("not found");
    System.out.println(first);
}
```

In the example, we find the first word that starts with "w".  


## The findAny method

In the next example, we use the `findAny` method.  

```java
import java.util.List;

void main() {

    var words = List.of(
            new User("John Doe", "gardener"),
            new User("Roger Roe", "driver"),
            new User("Jozef Kral", "shopkeeper"),
            new User("Boris Brezov", "musician"),
            new User("Lucia Novak", "teacher"));

    var res = words.stream().filter(u -> u.occupation().equals("gardener"))
            .findAny();

    res.ifPresent(System.out::println);
}

record User(String name, String occupation) {
}
```

We have a list of users. We find out if there is any user who is a gardener.  

