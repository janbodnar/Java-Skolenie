# Samples

## Read CSV files

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.Arrays;

void main() throws IOException {

    Path path= Paths.get("src/resources/data.csv");

    String contents = Files.readString(path);

//    String regex = "[,\\s]+";
    String regex = ",";
    String[] parts = contents.split(regex);

    System.out.println(Arrays.toString(parts));

    int sum = 0;

    for (String part : parts) {


        sum += Integer.parseInt(part.trim());
    }

    System.out.println(sum);

}
```




```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>FirstUIEx</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>22</maven.compiler.source>
        <maven.compiler.target>22</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>


    <dependencies>
        <dependency>
            <groupId>org.openjfx</groupId>
            <artifactId>javafx-controls</artifactId>
            <version>22-ea+11</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.openjfx</groupId>
                <artifactId>javafx-maven-plugin</artifactId>
                <version>0.0.8</version>
                <configuration>
                    <mainClass>org.example.FirstEx</mainClass>
                </configuration>
            </plugin>
        </plugins>
    </build>

</project>
```


## removeIf Map

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

    capitals.entrySet().removeIf(entry -> !entry.getValue().startsWith("B"));

    System.out.println(capitals);

}
```



## removeIf List

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    List<String> words = new ArrayList<>();
    words.add("sky");
    words.add("atom");
    words.add("war");
    words.add("cloud");
    words.add("tent");
    words.add("water");
    words.add("warm");
    words.add("ocean");

    // ascii velkost su 3 znaky
    // slova zacinajuce na w alebo c

//    values.removeIf(val -> val < 0);
//    words.removeIf(word -> word.length() == 3);

    words.removeIf(word -> word.startsWith("w") || word.startsWith("c"));

    System.out.println(words);
}
```


## enum

```java
enum Season {
    SPRING,
    SUMMER,
    AUTUMN,
    WINTER
}


void main() {

    Season s1 = Season.AUTUMN;
    System.out.println(s1);

    Season s2 = Season.WINTER;
    System.out.println(s2);

    for (Season season : Season.values()) {
        System.out.println(season);
    }
}
```


## and/or operators 

```java
void main() {

    String[] words = {"sky", "war", "atom", "water", "warm", "cup", "cloud"};

    for (String word : words) {

        if (word.startsWith("w") && (word.length() == 3 || word.length() == 4)) {

            System.out.println(word);
        }
    }
}
```

---

```java
void main() {

    int[] vals = {1, -2, 0, 1, -1, 5, 10, -6};

    for (int val : vals) {

        if (val % 2 == 0 && val < 0) {
            System.out.println(val);
        }
    }
}
```


## and operator

```java
void main() {


    String[] words = {"sky", "war", "atom", "water", "warm", "cup", "cloud"};

    for (String word : words) {

        if (word.startsWith("w") || word.startsWith("c") ) {

            System.out.println(word);
        }

    }
}
```


## Sum for loop

```java
void main() {

    int[] vals = {10, 25, 30, 45, 50};
    int sum = 0;

    for (int i = 0; i < vals.length; i++) {

        sum = sum + vals[i];
    }

    System.out.println(sum);
}
```

## Even/odd sum

```java
void main() {

    int[] vals = {10, 25, 30, 45, 50};
    int sum = 0;

    for (int val : vals) {
        if (val % 2 == 1) {
            sum = sum + val;

        }
    }

    System.out.println(sum);
}
```

## Recap

```java
void main() {

    String name = "John Doe";
    int age = 34;
    String occupation = "gardener";

    System.out.printf("%s is %d years old and he is a %s%n", name, age, occupation);
    System.out.println(name + " is " + age + " years old and he is a " + occupation);

    String message = String.format("%s is %d years old and he is a %s%n", name, age, occupation);
    System.out.println(message);
}
```
