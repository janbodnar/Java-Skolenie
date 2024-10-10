# Priklady

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
