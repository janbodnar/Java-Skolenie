# Basic I/O operations

We use high-level methods from the `Files` class.  

## Read input 

We can use `Scanner` to read input from users.  

```java
import java.util.Scanner;

void main() {

    try (var scanner = new Scanner(System.in)) {

        System.out.print("Enter your name: ");
        String name = scanner.nextLine(); // Read a line of text (including spaces)

        String msg = "Hello %s".formatted(name);
        System.out.println(msg);
    }
}
```

## Create file 

`Files.exists` - to check if a file exists  
`Files.createFile` - to create a file  

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

void main() throws IOException {

    Path myPath = Paths.get("src/resources/words.txt");

    if (Files.exists(myPath)) {

        System.out.println("File already exists");
    } else {

        Files.createFile(myPath);
        System.out.println("File created");
    }
}
```

## File size 

`Files.size` - to get the size of a file.  

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

void main() throws IOException {

    Path myPath = Paths.get("src/resources/bugs.txt");
    long fileSize = Files.size(myPath);

    System.out.format("File size: %d bytes%n", fileSize);
}
```

## Delete file 

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

void main() throws IOException {

    Path myPath = Paths.get("src/resources/myfile.txt");
    boolean fileDeleted = Files.deleteIfExists(myPath);

    if (fileDeleted) {

        System.out.println("File deleted");
    } else {

        System.out.println("File does not exist");
    }
}
```

## Read file 

`Files.readAllLines` - read lines into a list of strings  
`Files.readString` - read data into a String  

```java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.List;

void main() throws IOException {

    Path myPath = Paths.get("src/resources/bugs.txt");

    List<String> lines = Files.readAllLines(myPath, StandardCharsets.UTF_8);
    lines.forEach(System.out::println);

    // suitable for small files
    String content = Files.readString(myPath, StandardCharsets.UTF_8);
    System.out.println(content);
}
```


## Write to file 

```java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.nio.file.StandardOpenOption;
import java.util.ArrayList;
import java.util.List;

void main() throws IOException {

    Path myPath = Paths.get("src/resources/myfile.txt");

    List<String> lines = new ArrayList<>();
    lines.add("blue sky");
    lines.add("sweet orange");
    lines.add("fast car");
    lines.add("old book");

    Files.write(myPath, lines, StandardCharsets.UTF_8,
            StandardOpenOption.CREATE, StandardOpenOption.TRUNCATE_EXISTING);

    System.out.println("Data written");
}
```

## Copy file 

```java
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.StandardCopyOption;

void main() throws IOException {

    var source = new File("src/resources/bugs.txt");
    var dest = new File("src/resources/bugs2.txt");

    Files.copy(source.toPath(), dest.toPath(),
            StandardCopyOption.REPLACE_EXISTING);
}
```
