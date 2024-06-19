# List directory contents


*Directory* is an organizing unit in a computer's file system for storing and  
locating files. Directories are hierarchically organized into a tree of  
directories. Directories have parent-child relationships.  

## Non-recursively with Files.list

The `Files.list` method returns a lazily populated stream of `Path` objects. The  
listing is not recursive.  

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.stream.Stream;

void main() throws IOException {

    String dirName = "..";

    try (Stream<Path> filesStream = Files.list(Paths.get(dirName))) {
        filesStream.limit(10).forEach(System.out::println);
    }
}
```

This example displays ten files or directories from the given directory.  


## Recursively with Files.walk

The `Files.walk` method returns a lazily populated stream of `Paths` by walking  
the file tree rooted at a given starting file. `Files.walk` recursively walks  
all subdirectories.  

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.stream.Stream;

void main() throws IOException {

    String pathName = "..";

    try (Stream<Path> paths = Files.walk(Paths.get(pathName))) {
        paths.filter(Files::isRegularFile)
                .forEach(System.out::println);
    }
}
```

This example displays the contents of the given directory with `Files.walk`  
method. With the filter method, we filter the contents of the directory to  
include only regular files.  

## Non-recursively with Files.walkFileTree

`Files.walkFileTree` method walks a file tree rooted at a given starting file.  
It uses a `FileVisitor` pattern which specifies the required behavior at key  
points in the traversal process: when a file is visited, before a directory is  
accessed, after a directory is accessed, or when a failure occurs.  

```java
import java.io.File;
import java.io.IOException;
import java.nio.file.FileVisitResult;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.SimpleFileVisitor;
import java.nio.file.attribute.BasicFileAttributes;
import java.util.Collections;

void main() throws IOException {

    String dirName = "..";
    File file = new File(dirName);

    Files.walkFileTree(file.toPath(), Collections.emptySet(), 1, new SimpleFileVisitor<>() {
        @Override
        public FileVisitResult visitFile(Path file, BasicFileAttributes attrs) {
            System.out.println(file);
            return FileVisitResult.CONTINUE;
        }
    });
}
```

The example uses `Files.walkFileTree` to traverse a directory non-recursively.  

```java
Files.walkFileTree(file.toPath(), Collections.emptySet(), 1, new SimpleFileVisitor<Path>() {
```

The `Files.walkFileTree` parameters are: the starting file, the options to  
configure the traversal, the maximum number of directory levels to visit, the  
file visitor to invoke for each file. In our case we have one directory level to  
traverse.  

## Recursively with Files.walkFileTree

In the following example, we use `Files.walkFileTree` to traverse the whole  
directory structure.  

```java
import java.io.File;
import java.io.IOException;
import java.nio.file.FileVisitResult;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.SimpleFileVisitor;
import java.nio.file.attribute.BasicFileAttributes;

void main() throws IOException {

    String dirName = "..";
    File file = new File(dirName);

    Files.walkFileTree(file.toPath(), new SimpleFileVisitor<>() {
        @Override
        public FileVisitResult visitFile(Path file, BasicFileAttributes attrs) {
            System.out.println(file);
            return FileVisitResult.CONTINUE;
        }
    });
}
```

The example uses an overloaded `Files.walkFileTree` method to traverse a  
directory recursively.  

## Non-recursively with File

The `java.io.File` class is an older API to list directory contents. It is not as  
powerful as the modern API, mentioned earlier. The File's `listFiles` returns an  
array of file objects in the given directory.  

```java
import java.io.File;

void main() {

    String dirName = "..";

    File fileName = new File(dirName);
    File[] fileList = fileName.listFiles();

    if (fileList != null) {
        for (File file : fileList) {
    
            System.out.println(file);
        }
    }
}
```

The example prints the contents of the given directory to the console. It does  
not go into subdirectories.  

## Recursively with File

This time we use `java.io.File` class to recursively list the directory.

```java
import java.io.File;
import java.util.ArrayList;
import java.util.List;

List<File> files = new ArrayList<>();

void main() {

    String dirName = "..";
    File file = new File(dirName);

    List<File> myfiles = doListing(file);
    myfiles.forEach(System.out::println);
}

List<File> doListing(File dirName) {

    File[] fileList = dirName.listFiles();

    if (fileList != null) {
        for (File file : fileList) {

            if (file.isFile()) {

                files.add(file);
            } else if (file.isDirectory()) {

                files.add(file);
                doListing(file);
            }
        }
    }

    return files;
}
```

The `doListing` method lists the contents of a directory. We determine if the  
file is a directory with `isDirectory` method and recursively call `doListing` on  
each subdirectory.  
