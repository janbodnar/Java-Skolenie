# Priklady


## forEach funkcia

```java
void main() {

    // vypis slova zacinajuce sa na w
    // vypis slova majuce tri pismena
    List<String> words = List.of("sky", "blue", "water", "nord", "small", "war");

    words.forEach(w -> {
        if (w.startsWith("w")) {
            System.out.println(w);
        }
    });

    words.forEach(w -> {
        if (w.length() == 3) {
            System.out.println(w);
        }
    });
}
```


## Opakovanie

```java
void main() {

    // vypis hlasku John Doe is 45 years old and he is a gardener
    String name = "John Doe";
    int age = 45;
    String occupation = "gardener";


    // vypis slova zacinajuce sa na w
    // vypis slova majuce tri pismena
    List<String> words = List.of("sky", "blue", "nord", "small", "war");

    // vypocitaj sumu
    int[] vals = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};   
}
```



## Podmienene vypisanie hodnot pola

```java
void main() {

    String[] planets = {
            "Mercury", "Venus", "Earth",
            "Mars", "Jupiter", "Saturn", "Uranus", "Pluto"
    };

// Vypis planety zacinajuce na M alebo S
    for (String planet : planets) {

        if (planet.startsWith("M") || planet.startsWith("S") ) {
            System.out.println(planet);
        }
    }
}
```



## Sum array of integers 

```java
void main() {

    int[] vals = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

//    System.out.println(vals[0]);
//    System.out.println(vals[1]);
//    System.out.println(vals[2]);
//
//    System.out.println(vals[vals.length-1]);

    int vals_len = vals.length;

    int sum = 0;

    for (int i = 0; i < vals_len; i++) {

        sum = sum + vals[i];
    }

    System.out.println(sum);
}
```


## Random vals

```java
import java.util.Random;

void main() {

    var r = new Random();
    int num = r.nextInt(7) - 3;

    if (num > 0) {

        System.out.println("The number is positive");
    } else if (num < 0) {

        System.out.println("The number is negative");
    } else {
        System.out.println("The number is zero");
    }

//    if (num < 0) {
//        System.out.println("The number is negative");
//    }
//
//    if (num == 0) {
//        System.out.println("The number is zero");
//    }

}
```


## Program

```java
package me.webcode;

import java.util.List;

public class Program {

    void main() {

        List<String> words = List.of("sky", "storm");

        for (String word : words) {
            System.out.println(word);
        }

        int x = 10;
        int y = 11;
        int z = x + y;

        System.out.println(z);
    }
}
```


## Get ages of users

```java
import org.jdbi.v3.core.Jdbi;
import org.jdbi.v3.core.mapper.reflect.ConstructorMapper;

import java.util.List;

void main() {

    String jdbcUrl = "jdbc:postgresql://localhost:5432/testdb";
    String username = "postgres";
    String password = "postgres";

    Jdbi jdbi = Jdbi.create(jdbcUrl, username, password);

    List<User> users = jdbi.withHandle(handle -> handle.select("SELECT * FROM users")
            .registerRowMapper(User.class, ConstructorMapper.of(User.class))
            .mapTo(User.class)
            .list());

    if (users.isEmpty()) {

        System.out.println("No users found.");
    } else {

        System.out.println("found " + users.size() + " users");
    }

    for (User user: users) {

        LocalDate currentDate = LocalDate.now();
        LocalDate birthDate = LocalDate.parse(user.dob);
        Period age = Period.between(birthDate, currentDate);

        System.out.printf("%s %s is %d years old%n", user.first_name, user.last_name, age.getYears());
    }
}

public record User(int id, String first_name, String last_name, String occupation, String dob) {
}
```


```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="format.css">
    <title>My html page</title>
</head>
<body>

<a href="https://wikipedia.org">Wikipedia.org</a>

<p>Today is a beautiful day. We go swimming and fishing.</p>
<p>Hello there. How are you?</p>

<a href="https://youtube.com">Youtube</a>

</body>
</html>
```


## Get h1 from webpage

```java
package com.zetcode;

import java.io.IOException;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;

public class JSoupMetaInfoEx {

    public static void main(String[] args) throws IOException {

        String url = "https://wikipedia.sk";
        Document document = Jsoup.connect(url).get();

        Element h1tag = document.select("h1").first();

        if (h1tag != null) {
            String h1text = h1tag.text();
            System.out.println(h1text);
        } else {
            System.out.println("h1 tag not found");
        }
    }
}
```

## Regex 

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Optional;
import java.util.OptionalDouble;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main () {
    
    // calculate sum
    
    String data = """
            1;2;12,  4,5 ,6,  7;2;3
            1;2;6; 15;2;5;6;7;34
            """;

    Pattern pattern = Pattern.compile("[,;\\s]+");

    int suma = pattern.splitAsStream(data).mapToInt(Integer::valueOf).sum();
    System.out.println(suma);
    
    // calculate average
    String data2 = """
            | Jozef Novak 1230 |
            | John Doe 2340    |
            | Paul Smith 1234  |
            | Lucia Novak 1224 |
            """;

    Pattern pattern2 = Pattern.compile("\\d+");

    Matcher matcher = pattern2.matcher(data2);

    List<Integer> values = new ArrayList<>();

    while (matcher.find()) {
        int val = Integer.parseInt(matcher.group());
        values.add(val);
    }

    System.out.println(values);

    OptionalDouble avg = values.stream().mapToDouble(Double::valueOf).average();
    avg.ifPresent(System.out::println);


    // pick phrases that contain dog, falcon or night
    
    String data3 = """
            a new coin
            an old falcon
            a small house
            a stormy night
            a new costume
            a happy dog
            """;

//    Pattern pattern = Pattern.compile("dog|falcon|night");
//    List<String> found = data3.lines().filter(word -> pattern.matcher(word).find()).toList();
    List<String> found = data3.lines().filter(word -> word.matches(".* dog|.* falcon|night")).toList();
    System.out.println(found);
}
```


## Recap

```java
void main () {

    String data = """
            1;2;12,4,5,6,7;2;3
            1;2;6;15;2;5;6;7;34
            """;

    // compute sum of values

    String data2 = """
            | Jozef Novak 1230 |
            | John Doe 2340    |
            | Paul Smith 1234  |
            | Lucia Novak 1224 |
            """;

    // Compute average

    String data3 = """
            a new coin
            an old falcon
            a small house
            a stormy night
            a new costume
            a happy dog
            """;
    
    // pick phrases that contain dog, falcon or night

}
```

## Get date from JSON

```java
import com.google.gson.Gson;

import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;


void main() throws IOException, InterruptedException {

    String webPage = "http://time.jsontest.com";
    URI uri = URI.create(webPage);

    try (HttpClient client = HttpClient.newHttpClient()) {

        HttpRequest request = HttpRequest.newBuilder(uri).GET().build();
        String body = client.send(request, HttpResponse.BodyHandlers.ofString()).body();

        Gson gson = new Gson();
        TimeData td = gson.fromJson(body, TimeData.class);

        System.out.println(td);
    }
}

record TimeData(String time, Long milliseconds_since_epoch, String date) {
}
```


```json
[
  {
    "firstName": "John",
    "lastName": "Doe",
    "occupation": "gardener"
  },
  {
    "firstName": "Roger",
    "lastName": "Roe",
    "occupation": "teacher"
  },
  {
    "firstName": "Paul",
    "lastName": "Novak",
    "occupation": "programmer"
  }
]
```


## Json

```java
import com.google.gson.Gson;

void main() {

    Map<Integer, String> colours = new HashMap<>();
    colours.put(1, "blue");
    colours.put(2, "yellow");
    colours.put(3, "green");

    Gson gson = new Gson();
    String output = gson.toJson(colours);
    System.out.println(output);

    List<String> words = List.of("sky", "blue", "atom");

    String output2 = gson.toJson(words);
    System.out.println(output2);

    List<User> users = List.of(new User("John", "Doe", "gardener"),
            new User("Roger", "Roe", "teacher"),
            new User("Paul", "Novak", "programmer"));

    String output3 = gson.toJson(users);
    System.out.println(output3);

}

record User(String firstName, String lastName, String occupation) {
}
```


## Filter nulls

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    List<String> words = new ArrayList<>() {{
        add("sky");
        add(null);
        add("blue");
        add(null);
        add("cloud");
        add(null);
        add("ocean");
    }};

    List<String> cleaned = words.stream().filter(word -> word != null).toList();

    cleaned.forEach(word -> {
        System.out.printf("The %s word has %d letters%n", word, word.length());
    });
}
```

## Regex words from web

```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
import java.util.stream.Stream;

void main() throws IOException, InterruptedException {

    var uri = URI.create("https://www.mit.edu/~ecprice/wordlist.10000");

    try (HttpClient client = HttpClient.newHttpClient()) {

        HttpRequest request = HttpRequest.newBuilder(uri).GET().build();
        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

        Pattern pattern = Pattern.compile(".{10}");
        String body = response.body();

        List<String> lines = body.lines().toList();
        List<String> found = new ArrayList<>();

        for (String line : lines) {
            Matcher m = pattern.matcher(line);

            if (m.matches()) {
                found.add(line);
            }
        }

        System.out.println(found.size());

        Path path = Path.of("src/resources/words_10.txt");
        Files.write(path, found);

//        Path path = Path.of("src/resources/words.txt");
//        Files.writeString(path, body);

    }
}
```


## Regex, extrahovanie dat

```java
import java.util.ArrayList;
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    var sites = List.of("webcode.me", "zetcode.com", "freebsd.org", "netbsd.org");

    List<String> topLevels = new ArrayList<>();
    List<String> secondLevels = new ArrayList<>();

    Pattern p = Pattern.compile("(\\w+)\\.(\\w+)");

    for (var site: sites) {

        Matcher matcher = p.matcher(site);

        while (matcher.find()) {

            topLevels.add(matcher.group(1));
            secondLevels.add(matcher.group(2));
        }
    }

    System.out.println(topLevels);
    System.out.println(secondLevels);
}
```


## Stream pole

```java
import java.util.Arrays;

void main(String[] args)  {
    
    int[] vals = {-3, -2, 11, 2, 3, 4, 5, 0, -6, 7, 8, 9, 10};

    long len = Arrays.stream(vals).count();
    System.out.println(len);

    long suma = Arrays.stream(vals).sum();
    System.out.println(suma);

    long minVal = Arrays.stream(vals).min().getAsInt();
    System.out.println(minVal);

    long maxVal = Arrays.stream(vals).max().getAsInt();
    System.out.println(maxVal);
}
```



## Text na slova

```java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.List;
import java.util.regex.Pattern;

void main() throws IOException {

    Path myPath = Paths.get("src/resources/thermopylae.txt");
    String content = Files.readString(myPath, StandardCharsets.UTF_8);

    Pattern pattern = Pattern.compile("[\\s,.]+");
    List<String> words = pattern.splitAsStream(content).toList();

    System.out.println(words);
}
```


## Filtrovanie slov

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.List;
import java.util.stream.Stream;

void main() throws IOException {

    String fileName = "words.txt";

    Path path = Path.of(fileName);

    try (Stream<String> lines = Files.lines(path)) {

        List<String> words = lines.filter(word -> word.length() == 3).toList();

        words.forEach(System.out::println);
    }
}
```
