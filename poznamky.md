# Java poznamky

## Kosher kod na pracu s databazou

`Main.java`:  

```java
package org.example;


public class Main {

    public static void main(String[] args) {

        Program program = new Program();
        program.run();
    }
}
```

`Program.java`:  

```java
package org.example;

import java.sql.*;
import java.util.ArrayList;
import java.util.List;
import java.util.logging.Level;
import java.util.logging.Logger;

public class Program {

    String username = "postgres";
    String password = "postgres";
    String query = "SELECT * FROM countries";

    public void run() {

        List<Country> countries = getData();
        processData(countries);
    }

    private List<Country> getData() {

        List<Country> countries = new ArrayList<>();

        try (Connection con = DriverManager.getConnection("jdbc:postgresql://localhost:5432/testdb",
                username, password);
             PreparedStatement pst = con.prepareStatement(query);
             ResultSet rs = pst.executeQuery()) {

            while (rs.next()) {

                countries.add(new Country(rs.getInt(1), rs.getString(2),
                        rs.getInt(3)));
            }

        } catch (SQLException ex) {

            Logger lgr = Logger.getLogger(getClass().getName());
            lgr.log(Level.SEVERE, ex.getMessage(), ex);
        }
        return countries;
    }

    private void processData(List<Country> countries) {

        countries.stream().limit(10).forEach(System.out::println);
        System.out.println("------------------------");
        countries.stream().filter(country -> country.population() > 500_000_000).forEach(System.out::println);
    }
}

record Country(int id, String name, int population) {
}
```








## Parsovanie CSV suboru z webu

```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.util.ArrayList;
import java.util.List;

void main() throws IOException, InterruptedException {

    List<User> users = new ArrayList<>();

    URI uri = URI.create("https://webcode.me/users.csv");
    HttpRequest request = HttpRequest.newBuilder(uri).build();

    try (HttpClient client = HttpClient.newHttpClient()) {

        String content = client.send(request, HttpResponse.BodyHandlers.ofString()).body();
        System.out.println(content.lines().toList());

        List<String> lines = content.lines().skip(1).limit(100).toList();

        lines.forEach(line -> {

            String[] fields = line.split(",", 4);
            User user = new User(Integer.parseInt(fields[0]), fields[1], fields[2], fields[3]);
            users.add(user);
        });

        users.stream().limit(10).forEach(user -> System.out.printf("%s %s, %s%n", user.firstName(),
                user.lastName(), user.occupation()));
    }
}

record User(int id, String firstName, String lastName, String occupation) {
}
```




## Filter with enums

```java
import java.util.List;

void main() {

    List<User> users = List.of(
            new User("Jack", "jack234@gmail.com", MaritalStatus.DIVORCED),
            new User("Peter", "pete2@post.com", MaritalStatus.SINGLE),
            new User("Lucy", "lucy17@gmail.com", MaritalStatus.DIVORCED),
            new User("Robert", "bob56@post.com", MaritalStatus.MARRIED),
            new User("Martin", "mato4@imail.com", MaritalStatus.MARRIED)
    );

    List<User> res = users.stream()
            .filter(user -> user.maritalStatus() == MaritalStatus.MARRIED)
            .toList();

    res.forEach(p -> System.out.println(p.name()));
}

record User(String name, String email, MaritalStatus maritalStatus) {
}

enum MaritalStatus {
    SINGLE,
    MARRIED,
    DIVORCED
}
```


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


