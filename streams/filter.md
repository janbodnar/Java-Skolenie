# Filtering

A stream is a sequence of elements from a source that supports aggregate  
operations. Streams do not store elements; the elements are computed on demand.  
Elements are consumed from data sources such as collections, arrays, or I/O  
resources.  

Stream aggregate operations are similar to SQL operations. We can apply  
filtering, mapping, reducing, matching, searching, or sorting operations on  
streams. Streams allow chaining of multiple stream operations. Unlike  
collections which use external iterations, streams are iterated internally.  

The `filter` method is an intermediate operation, which returns elements of the  
stream that match the given predicate. A predicate is a function that returns a  
boolean value.  

## Filter string length

The following example filters a list of strings.  

```java
import java.util.List;

void main() {

    List<String> words = List.of("pen", "custom", "orphanage",
            "forest", "bubble", "butterfly");

    List<String> res = words.stream().filter(word -> word.length() > 5)
            .toList();

    res.forEach(System.out::println);
}
```

We have a list of words. We filter the list to include only strings whose length  
is bigger than five.  

```java
List<String> res = words.stream().filter(word -> word.length() > 5)
        .collect(Collectors.toList());
```

With the `stream` method, we create a Java Stream from a list of strings. On  
this stream, we apply the `filter` method. The `filter` method accepts an  
anonymous functions that returns a boolean `true` for all elements of the stream  
whose length is bigger that five. We create a list back from the stream with the  
collect method.  

```java
res.forEach(System.out::println);
```

We go through the result with the `forEach` method and print all its elements to  
the console.  


## Filter null values

The next example filters out null values.  

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

void main() {

    List<String> words = Arrays.asList("cup", null, "forest",
            "sky", "book", null, "theatre");

    List<String> res = words.stream().filter(w -> w != null)
            .collect(Collectors.toList());

    System.out.println(res);
}
```

We have a list of words. With the `Stream` filtering operation, we create a new  
list with null values removed.  

```java
List<String> res = words.stream().filter(w -> w != null)
        .collect(Collectors.toList());
```

In the body of the lambda expression, we check that the value is not null. The  
collect method is a terminal operation that creates a list from the filtered  
stream.  

## Multiple filter operations

It is possible to apply multiple filter operations on a stream.  

```java
import java.util.Arrays;
import java.util.function.IntConsumer;

void main() {

    int[] inums = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15 };
    
    IntConsumer icons = i -> System.out.print(i + " ");
    
    Arrays.stream(inums).filter(e -> e < 6 || e > 10)
            .filter(e -> e % 2 == 0).forEach(icons);
}
```

In the example, we apply multiple filter operations on a stream of integers.

```java
int[] inums = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15 };
```

We have an array of integer values.

```java
IntConsumer icons = i -> System.out.print(i + " ");
```

`IntConsumer` is an operation that accepts a single integer value argument and  
returns no result.  

```java
Arrays.stream(inums).filter(e -> e < 6 || e > 10)
        .filter(e -> e % 2 == 0).forEach(icons);
```

A stream is created from the array with the `Arrays.stream` method. Multiple  
filtering operations are performed.  

## Filter objects

The next example shows how to filter objects.  

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

The example creates a stream of `User` objects. It filters those which match a  
specific regular expression.  

```java
List<User> res = users.stream()
        .filter(user -> user.email().matches(".*post.com"))
        .toList();
```

In the filter predicate, we choose emails that match the `.*post.com` pattern.

## Filter map by keys

In the following example, we filter a map by its keys.  

```java
import java.util.HashMap;
import java.util.Map;

void main() {

    Map<String, String> hmap = new HashMap<>();

    hmap.put("de", "Germany");
    hmap.put("hu", "Hungary");
    hmap.put("sk", "Slovakia");
    hmap.put("si", "Slovenia");
    hmap.put("so", "Somalia");
    hmap.put("us", "United States");
    hmap.put("ru", "Russia");

    hmap.entrySet().stream().filter(map -> map.getKey().startsWith("s"))
            .forEach(System.out::println);
}
```

The example filters domain names starting with s letter.

## Filter map by values

In the following example, we filter a map by its values.  

```java
import java.util.HashMap;
import java.util.Map;

void main() {

    Map<String, String> hmap = new HashMap<>();

    hmap.put("de", "Germany");
    hmap.put("hu", "Hungary");
    hmap.put("sk", "Slovakia");
    hmap.put("si", "Slovenia");
    hmap.put("so", "Somalia");
    hmap.put("us", "United States");
    hmap.put("ru", "Russia");

    hmap.entrySet().stream().filter(map -> map.getValue().equals("Slovakia")
            || map.getValue().equals("Slovenia"))
            .forEach(System.out::println);
}
```

In the example, we filter out two countries from the map.  
