# Filtering ArrayList 


## A list of words

Using for loop.  

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    var words = List.of("sky", "tent", "war", "water", "warm",
            "cup", "cloud", "pen", "forest", "atom", "peril", "wood", "falcon");

    var filtered = new ArrayList<String>();

    for (var word : words) {
        if (word.startsWith("w")) {
            filtered.add(word);
        }
    }
    filtered.forEach(System.out::println);
}
```

Using streams.  

```java
import java.util.List;

void main() {

    var words = List.of("sky", "tent", "war", "water", "warm",
            "cup", "cloud", "pen", "forest", "atom", "peril", "wood", "falcon");

    var res = words.stream().filter(word -> word.startsWith("w")).toList();
    res.forEach(System.out::println);
}
```

## User's age

Using for loop.  

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    var p1 = new User("Michael", 23, Gender.MALE);
    var p2 = new User("Jane", 24, Gender.FEMALE);
    var p3 = new User("John", 44, Gender.MALE);
    var p4 = new User("Peter", 54, Gender.MALE);
    var p5 = new User("Lucy", 35, Gender.FEMALE);

    var users = List.of(p1, p2, p3, p4, p5);
    var res = new ArrayList<User>();

    for (User user : users) {
        if (user.age() > 30) {
            res.add(user);
        }
    }

    System.out.println(res);
}

enum Gender {
    MALE, FEMALE
}

record User(String name, int age, Gender gender) {
}
```

Using streams.  

```java
import java.util.List;

void main() {

    var p1 = new User("Michael", 23, Gender.MALE);
    var p2 = new User("Jane", 24, Gender.FEMALE);
    var p3 = new User("John", 44, Gender.MALE);
    var p4 = new User("Peter", 54, Gender.MALE);
    var p5 = new User("Lucy", 35, Gender.FEMALE);

    var users = List.of(p1, p2, p3, p4, p5);
    var res = users.stream().filter(u -> u.age > 30).toList();

    res.forEach(System.out::println);
}

enum Gender {
    MALE, FEMALE
}

record User(String name, int age, Gender gender) {
}
```





