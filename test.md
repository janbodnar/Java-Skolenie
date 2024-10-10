# Priklady

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
