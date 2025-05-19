# Priklady

## Contains key/value

```java
import java.util.HashMap;
import java.util.Map;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    String key1 = "ger";
    String key2 = "rus";

    String value1 = "Trnava";

    if (!capitals.containsValue(value1)) {
        System.out.println("Hashmap does not contain value " + value1);
    } else {
        System.out.println("Hashmap does contain value " + value1);
    }


    if (capitals.containsKey(key1)) {

        System.out.printf("HashMap contains %s key%n", key1);
    } else {

        System.out.printf("HashMap does not contain %s key%n", key1);
    }

    if (capitals.containsKey(key2)) {

        System.out.printf("HashMap contains %s key%n", key2);
    } else {

        System.out.printf("HashMap does not contain %s key%n", key2);
    }
}
```



## Reading files

```java
void main() throws IOException {

//    String fileName = "words.txt";
//    String fileName = "C:/Users/bodnar//IdeaProjects/SimpleEx/words.txt";
//    String fileName = "C:\\Users\\bodnar\\IdeaProjects\\SimpleEx\\words.txt";

    String fileName = "C:/Users/bodnar/Documents/words.txt";

    List<String> lines = Files.readAllLines(Paths.get(fileName));
    lines.forEach(line -> System.out.println(line.toUpperCase()));

    for (String line: lines) {
        System.out.println(line.length());
    }


//    String content = Files.readString(Paths.get(fileName));
//
//    System.out.println(content);
//    String[] words = content.split("[\\s]+");

//    System.out.println(Arrays.toString(words));

}
```


## forEach loop

```java
void main() {

    List<String> words = List.of("sky", "blue", "cup", "ocean");

    words.forEach(word -> System.out.println(word.toUpperCase()));

    for (String word : words) {
        System.out.println(word.toUpperCase());
    }

}
```




## Sorting arrays

```java
import java.util.Arrays;

void main() {

    int[] a = { 5, 2, 4, 3, 1 };
    int[] sorted = Arrays.stream(a).sorted().toArray();

    System.out.println(Arrays.toString(sorted));
    System.out.println(Arrays.toString(a));

    int[] b = { 5, 2, 4, 3, 1 };
    Arrays.sort(b);
    System.out.println(Arrays.toString(b));
}
```


## Split with regex

```java
void main(String[] args) {

     // calculate sum
    String data2 = "1,2;3,4;5,6,7;8,9;10";
    int sum3 = 0;

    String[] fields = data2.split("[;,]");

    for (String field: fields) {

        sum3 += Integer.parseInt(field);
    }

    System.out.println(sum3);
}
```


## Replace and calculate

```java
void main(String[] args) {

     // calculate sum
    String data2 = "1,2;3,4;5,6,7;8,9;10";
    int sum3 = 0;

    String cleanedData = data2.replace(';', ',');
    
    String[] fields = cleanedData.split(",");

    for (String field: fields) {

        sum3 += Integer.parseInt(field);
    }

    System.out.println(sum3);

}
```





## Opakovanie

```java
void main(String[] args) {

    // print message: John Doe is 34 years old, he is a gardener
    String name = "John Doe";
    int age = 34;
    String occupation = "gardener";

    // calculate sum using for loop
    // print first, second, last, last but one elements
    var vals = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
    // calculate sum of values 20..50, both inclusive
    // using while loop

    // print first, second, last, last but one element
    int[] data = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

    // calculate sum
    String data2 = "1,2,3,4,5,6,7,8,9,10";

}
```


## Riesenia

```java
    // print message: John Doe is 34 years old, he is a gardener
    String name = "John Doe";
    int age = 34;
    String occupation = "gardener";

    System.out.printf("%s is %d years old, he is a %s%n", name, age, occupation);

    String msg = String.format("%s is %d years old, he is a %s%n", name, age, occupation);
    System.out.println(msg);

    // calculate sum using for loop
    // print first, second, last, last but one elements
    List<Integer> vals = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

    int sum = 0;

    for (Integer val: vals) {
        sum += val;
    }

    System.out.println(sum);
    
    int first = vals.getFirst();
    int second = vals.get(1);
    int last = vals.getLast();
    int lastButOne = vals.get(vals.size() - 2);

    System.out.println(first);
    System.out.println(second);
    System.out.println(last);
    System.out.println(lastButOne);


    // calculate sum of values 20..50, both inclusive
    // using while loop

    int sum2 = 0;
    int i = 20;

    while (i <= 50) {

        sum2 += i;
        i++;
    }

    System.out.println(sum2);


    // print first, second, last, last but one element
    int[] data = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

    System.out.println(data[0]);
    System.out.println(data[1]);
    System.out.println(data[data.length - 1]);
    System.out.println(data[data.length - 2]);


     // calculate sum
    String data2 = "1,2,3,4,5,6,7,8,9,10";
    int sum3 = 0;
    
    String[] fields = data2.split(",");

    for (String field: fields) {

        sum3 += Integer.parseInt(field);
    }

    System.out.println(sum3);

```
















## Calculate sum of CSV data

```java
void main(String[] args) {

//   1. calculate sum
//   2. transform to 1;2;3;4;5;6;7;8;9;10
    String data = "1,2,3,4,5,6,7,8,9,10";

//    ["1", "2", .. "10"]
    String[] fields = data.split(",");
    int sum = 0;

    for (String field :fields) {
        sum += Integer.parseInt(field);
    }

    System.out.println(sum);

}
```


## Sum of program args

```java
void main(String[] args) {

    int sum = 0;

    for (String arg : args) {
        sum += Integer.parseInt(arg);
    }

    System.out.println(sum);
}
```


## split function

```java
void main() {

    String fullName = "John Doe";

    String[] parts = fullName.split(" ");

    String firstName = parts[0];
    String lastName = parts[1];

    System.out.println(firstName);
    System.out.println(lastName);

    System.out.println(fullName);
}
```


## and/or operators

```java
void main() {

    String[] words = {"war", "water", "cup", "snow", "pup", "cloud", "dog", "warm"};
    
    for (var word : words) {

        if (word.startsWith("w") || word.startsWith("c")) {
            System.out.println(word);
        }

        if (word.length() == 3 && word.startsWith("w")) {
            System.out.println(word);
        }
    }
}
```



## Opakovanie

```java
void main() {

    // print message John Doe is 45 years old
    String name = "John Doe";
    int age = 45;
    
    // calculate sum of 1..10 integers
    int[] vals = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    
    // print the following message 8 times using while loop
    String msg = "an old falcon";
    
    // print first, last, last but one elements
    // calculate the sum of lenghts
    String[] words = {"sky", "look", "pen", "snow", "car", "war"};
    
    // using classic for loop, generate 10 random numbers
    var random = new Random();
}
```

## Riesenia

```java
void main() {

    // print message John Doe is 45 years old
    String name = "John Doe";
    int age = 45;

    System.out.printf("%s is %d years old%n", name, age);
    System.out.println(name + " is " + age + " years old");

    // calculate sum of 1..10 integers
    int[] vals = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int sum = 0;

    for (int val : vals) {
        sum = sum + val;
    }

    System.out.println(sum);

    // print the following message 8 times using while loop
    String msg = "an old falcon";

    for (int i = 0; i < 8; i++) {
        System.out.println(msg);
    }

    int i = 0;

    while (i < 8) {
        System.out.println(msg);
        i++;
    }

    System.out.println("end of program");


    String[] words = {"sky", "look", "pen", "snow", "car", "war"};

    int len = words.length;

    System.out.println(words[0]);
    System.out.println(words[len-1]);
    System.out.println(words[len-2]);

    int sum_of_chars = 0;

    for (String word : words) {
        sum_of_chars += word.length();
    }

    System.out.println(sum_of_chars);

    System.out.println("end of program");

    // using classic for loop, generate 10 random numbers
    var random = new Random();

    for (int i = 0; i<10; i++) {

        int r = random.nextInt();
        System.out.println(r);
    }

}
```











## toString funkcia

```java
package com.zetcode;

class Person {

    public String firstName;
    public String lastName;
    public String occupation;

    @Override
    public String toString() {
        return "Person{" +
                "firstName='" + firstName + '\'' +
                ", lastName='" + lastName + '\'' +
                ", occupation='" + occupation + '\'' +
                '}';
    }
}

public class Main {

    public static void main(String[] args) {

        Person p1 = new Person();
        p1.firstName = "Jane";
        p1.lastName = "Doe";
        p1.occupation = "teacher";

        Person p2 = new Person();
        p2.firstName = "Roger";
        p2.lastName = "Roe";
        p2.occupation = "driver";

        System.out.println(p1);
        System.out.println(p2);

    }
}
```


## Map of planets

```java
void main() {

    Map<String, Double> planetDistances = new HashMap<>();

    // Adding planets and their distances from the Sun
    planetDistances.put("Mercury", 57.9);
    planetDistances.put("Venus", 108.2);
    planetDistances.put("Earth", 149.6);
    planetDistances.put("Mars", 227.9);
    planetDistances.put("Jupiter", 778.3);
    planetDistances.put("Saturn", 1427.0);
    planetDistances.put("Uranus", 2871.0);
    planetDistances.put("Neptune", 4497.1);

    // Printing the map
    planetDistances.forEach((planet, distance) ->
            System.out.println(planet + ": " + distance + " million km")
    );
}
```

## Fill arrays

```java
import java.util.Arrays;

void main() {

    int[] a = new int[10];

    System.out.println(Arrays.toString(a));
    Arrays.fill(a, 1);

    System.out.println(Arrays.toString(a));

    double[] b = new double[15];
    Random r = new Random();
    Arrays.setAll(b, idx -> r.nextDouble(10));

    System.out.println(Arrays.toString(b));

    float[] b2 = new float[15];
    Random r1 = new Random();

    for (int i = 0; i < b2.length; i++) {
        float randomFloat = r.nextFloat() * 100; // Generate a random float between 0 and 100
        float roundedFloat = Math.round(randomFloat * 100.0f) / 100.0f; // Round to two decimal places
        b2[i] = roundedFloat;
    }
    
    System.out.println(Arrays.toString(b2));
}
```

## Read CSV file

```java
void main() throws IOException {

    String fileName = "C:/Users/bodnar/Documents/data.csv";
    Path filePath = Path.of(fileName);

    List<String> lines = Files.readAllLines(filePath);

    int suma = 0;

    for (String line : lines) {

        String[] fields = line.split(";");


        for (String field : fields) {
            suma = suma + Integer.parseInt(field);
        }
    }

    System.out.println(suma);
}
```


## Suma z CSV dat

```java
void main() {

    String data = "1,2,3,4,5,6,7,8,9,10";
    String[] fields = data.split(",");

    int suma = 0;

    for (String field : fields) {
        suma = suma + Integer.parseInt(field);
    }

    System.out.println(suma);
```


## Stranky na riesenie uloh

- [leetcode.com](https://leetcode.com/)
- [www.codewars.com](https://www.codewars.com/)


## Frekvencia znakov v texte

```java
void main() {

    String text = """
            The Battle of Thermopylae was fought between an alliance of Greek city-states,
            led by King Leonidas of Sparta, and the Persian Empire of Xerxes I over the
            course of three days, during the second Persian invasion of Greece.
            """;

    Map<Character, Integer> charCountMap = new HashMap<>();

    for (char c : text.toCharArray()) {
        if (charCountMap.containsKey(c)) {
            charCountMap.put(c, charCountMap.get(c) + 1);
        } else {
            charCountMap.put(c, 1);
        }
    }

    charCountMap.forEach((key, value) -> System.out.println(key + ": " + value));
}
```


## Cleaning words

```java
import java.util.List;

void main() {

    var words = List.of("sky\n", "\nwar\n", "toy  ", "  blue", "\t\t", "", "sky");
    System.out.println(words);

    ArrayList<String> words_cleaned = new ArrayList<>();

    for (String word : words) {

        if (!word.isBlank()) {
            words_cleaned.add(word.trim());
        }
    }

    System.out.println(words_cleaned);
}
```


## Ternary operator

```java
void main() {
    int age = 31;

    boolean adult = age >= 18 ? true : false;
    
//    if (age >= 18) {
//        adult = true;
//    } else {
//        adult = false;
//    }

    System.out.println(String.format("Adult: %s", adult));
}
```

## suma a dnesny datum

```java
void main() {

    // vypocitaj sumu
    int[] vals = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

    int sum = 0;

    for (int val : vals) {
        sum = sum + val;
    }

    System.out.println(sum);
    System.out.println(Arrays.stream(vals).sum());

    // Vypis dnesny datum

    LocalDate today = LocalDate.now();
    System.out.println("Dnešný dátum je: " + today);

}
```

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
