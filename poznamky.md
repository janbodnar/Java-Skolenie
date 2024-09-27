# Java poznamky

## Sorting records

```java
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

    var sorted = users.stream().sorted(Comparator.comparing(User::lastName).reversed()).toList();

    sorted.forEach(System.out::println);
}

record User(String firstName, String lastName, int salary) {
}
```


## Sorting

```java
import java.util.Comparator;
import java.util.List;

void main() {

    List<String> words = List.of("sky", "pen", "new", "rock", "war", "water");
    System.out.println(words);

    List<String> filtered = words.stream().filter(word -> word.startsWith("w")).toList();
    System.out.println(filtered);

    List<String> sorted = words.stream().sorted(Comparator.naturalOrder()).toList();
    System.out.println(sorted);

    List<String> reversed = words.stream().sorted(Comparator.reverseOrder()).toList();
    System.out.println(reversed);
}
```


## forEach

```java
import java.util.Arrays;
import java.util.List;

void main() {

    List<String> words = List.of("sky", "pen", "new", "rock", "war", "water");

    System.out.println(words);

//    words.forEach(word -> System.out.println(word));
    words.forEach(System.out::println);
    
//    for (String word: words) {
//        System.out.println(word);
//    }

    int[] vals = {1, 2, 3, 4, 5};
    Arrays.stream(vals).forEach(System.out::println);
}
```


## Filtrovanie slov zo suboru

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;
import java.util.List;

void main() throws IOException {

    List<String> w_words = new ArrayList<>();
    List<String> w_c_words = new ArrayList<>();

    String fileName = "words.txt";
    Path filePath = Path.of(fileName);

    List<String> lines = Files.readAllLines(filePath);

    for (String line: lines) {

        if (line.startsWith("w")) {
            w_words.add(line);
        }
    }

    for (String line: lines) {

        if (line.startsWith("w") || line.startsWith("c") ) {
            w_c_words.add(line);
        }
    }

    System.out.println(w_words);
    System.out.println(w_c_words);
}
```


## Podmienecne vymazanie prvkov

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    List<String> words = new ArrayList<>();
    words.add("sky");
    words.add("atom");
    words.add("cup");
    words.add("war");
    words.add("water");
    words.add("new");
    words.add("ocean");

    words.removeIf(word -> !word.startsWith("w") );

    System.out.println(words);
}
```

Priklad vymaze elementy zo zoznamu, ktore sa nezacinaju na 'w'.


## Citanie suboru 

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.List;

void main() throws IOException {

    String fileName = "words.txt";
    Path filePath = Path.of(fileName);

    List<String> lines = Files.readAllLines(filePath);

    for (String line: lines) {

        System.out.printf("The word %s has %d characters%n", line,  line.length());
    }
}
```


Tento priklad ukazuje pouzitie pola.  

## Pole cisiel

```java
import java.util.Arrays;

void main() {

    int[] vals = {1, 2, 3, 4, 5, 6};

    // calculate sum
    int sum = 0;

    for (int val : vals) {
        sum += val;
    }

    System.out.println("The sum is: " + sum);

    int sum2 = Arrays.stream(vals).sum();
    System.out.println(sum2);

    // print first and last element

    System.out.println(vals[0]);
    System.out.println(vals[vals.length - 1]);

    // iterate array from the end

    for (int i=vals.length-1; i >= 0 ; i--) {

        System.out.println(vals[i]);
    }
}
```

## Hlavne okno

![IntelliJ Main](/images/intellij.png)


