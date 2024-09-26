# Java poznamky

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


