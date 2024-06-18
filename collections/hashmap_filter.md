# HashMap filter

`HashMap` is a container that stores key-value pairs. Each key is associated  
with one value. Keys in a `HashMap` must be unique.   

`HashMap` can be filtered with the filter method of the Java Stream API.  

# Filter map by values

In the first example, we filter the values of a map.

```java
import java.util.HashMap;
import java.util.Map;
import java.util.stream.Collectors;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    Map<String, String> filteredCapitals = capitals.entrySet().stream()
        .filter(e -> e.getValue().startsWith("B"))
        .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));

    filteredCapitals.entrySet().forEach(System.out::println);
}
```

We have a map of capitals. We get the entries of a map with `entrySet`. Then we  
turn the set into a stream with `stream`.  

```java
Map<String, String> filteredCapitals = capitals.entrySet().stream()
    .filter(e -> e.getValue().startsWith("B"))
    .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));
```

We filter the map to contain only pairs whose values start with B. We get the  
value from the current entry with `getValue`.  


## Filter map by keys

In the next example, we filter the map by its keys.

```java
Main.java
import java.util.HashMap;
import java.util.Map;
import java.util.stream.Collectors;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    Map<String, String> filteredCapitals = capitals.entrySet().stream()
        .filter(e -> e.getKey().endsWith("k"))
        .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));

    filteredCapitals.entrySet().forEach(System.out::println);
}
```

The example filters all entries whose keys end with letter k.  

```java
Map<String, String> filteredCapitals = capitals.entrySet().stream()
    .filter(e -> e.getKey().endsWith("k"))
    .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));
```

We get the current key of an entry with getKey.


## Filter map by keys and values

In the next example we filter a map by the keys and values.

```java
import java.util.HashMap;
import java.util.Map;
import java.util.stream.Collectors;

void main() {

    Map<Integer, String> users = new HashMap<>();

    users.put(1, "John Doe");
    users.put(2, "Roger Roe");
    users.put(3, "Jane Doe");
    users.put(4, "Jack Drake");
    users.put(5, "Peter Morgan");
    users.put(6, "Robert Melnik");

    Map<Integer, String> filtered = users.entrySet().stream()
            .filter(e -> e.getKey() % 2 == 0)
            .filter(e -> e.getValue().split(" ")[1].startsWith("D"))
            .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));

    filtered.entrySet().forEach(System.out::println);
}
```

We have a map of users. We filter out all users whose keys are even and whose  
lastnames start with letter D.  


## Filter by age

We have a map of users. We filter the map by the users' age.

```java
import java.util.Map;
import java.util.stream.Collectors;
import java.time.LocalDate;
import java.time.Period;
import java.time.format.DateTimeFormatter;
import java.util.HashMap;

void main() {

    var dft = DateTimeFormatter.ofPattern("yyyy-MM-dd");

    Map<Integer, User> users = new HashMap<>();
    users.put(1, new User("John Doe", "gardener", LocalDate.parse("1973-09-07", dft)));
    users.put(2, new User("Roger Roe", "driver", LocalDate.parse("1963-03-30", dft)));
    users.put(3, new User("Kim Smith", "teacher", LocalDate.parse("1980-05-12", dft)));
    users.put(4, new User("Joe Nigel", "artist", LocalDate.parse("1983-03-30", dft)));
    users.put(5, new User("Liam Strong", "teacher", LocalDate.parse("2009-03-06", dft)));
    users.put(6, new User("Robert Young", "gardener", LocalDate.parse("1978-11-16", dft)));
    users.put(7, new User("Liam Strong", "teacher", LocalDate.parse("1986-10-23", dft)));

    Map<Integer, User> olderThanForty = users.entrySet().stream().filter(e -> {
        LocalDate dob = e.getValue().dob();
        int age = Period.between(dob, LocalDate.now()).getYears();
        return age > 40;
    }).collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));

    olderThanForty.entrySet().forEach(System.out::println);
}

record User(String name, String occupation, LocalDate dob) {
}
```

We filter out all users that are older than forty.  

```java
Map<Integer, User> olderThanForty = users.entrySet().stream().filter(e -> {
    LocalDate dob = e.getValue().dob();
    int age = Period.between(dob, LocalDate.now()).getYears();
    return age > 40;
}).collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));
```

We retrieve the date of birth from the user object with `e.getValue().dob()`.  
Thenwe calculate the user's age with `Period.between(dob, LocalDate.now()).getYears()`.  
The filter condition is `age > 40`;  
