# Compile and run a Java program

This document shows the traditional workflow for compiling a Java source file,  
running the compiled class, running a source file directly, and packaging the  
program as an executable JAR file.  

## Requirements

Install a Java Development Kit (JDK). The JDK provides the `javac` compiler,  
the `java` launcher, and the `jar` packaging tool.  

Check that the tools are available in the terminal:  

```text
java --version
javac --version
jar --version
```

The commands in this document use the current directory as the project  
directory. Linux and macOS use `/` in paths. Windows uses `\` instead.  

## Project structure

Create a source directory and a directory for compiled classes. The `-p` option  
creates all missing parent directories on Linux and macOS:  

```text
mkdir -p src/main/java/com/example bin
```

On Windows PowerShell, use:  

```powershell
New-Item -ItemType Directory -Force src/main/java/com/example, bin
```

The project now has this structure:  

```text
project/
├── bin/
└── src/
    └── main/
        └── java/
            └── com/
                └── example/
                    └── Main.java
```

The directory structure follows the package declaration. The package  
`com.example` corresponds to the directories `com/example`.  

## Source code

Create `src/main/java/com/example/Main.java` with this content:  

```java
package com.example;

public class Main {

    public static void main(String... args) {
        System.out.println("Hello, Java!");
    }
}
```

The public class is named `Main`, so the source file must be named `Main.java`.  
The `main` method is the entry point used when the compiled application starts.  

## Compile

Compile the source file with `javac`:  

```text
javac -d bin src/main/java/com/example/Main.java
```

The `-d bin` option tells the compiler to place generated files in the `bin`  
directory. The compiler creates the package directories automatically and  
produces:  

```text
bin/
└── com/
    └── example/
        └── Main.class
```

The `.class` file contains Java bytecode. It is not normally opened directly;  
it is loaded and executed by the JVM.  

On Windows, the same command can use backslashes:  

```powershell
javac -d bin src\main\java\com\example\Main.java
```

## Run the compiled class

Run the program with the `java` launcher:  

```text
java -cp bin com.example.Main
```

The `-cp` option sets the class path. It tells the JVM to search for compiled  
classes in `bin`. The class name is written with dots because it includes the  
package name. Do not add the `.class` suffix:  

```text
com.example.Main     correct
com/example/Main.class  incorrect
```

The output is:  

```text
Hello, Java!
```

The class path points to the directory above the package directory. It points  
to `bin`, not to `bin/com/example`.  

## Run a source file directly

Recent JDK versions can launch a simple source file directly:  

```text
java src/main/java/com/example/Main.java
```

The `java` launcher compiles and runs the source file in one operation. This is  
convenient for small programs and experiments. It does not replace the  
explicit `javac` step when you need reusable `.class` files, a controlled build  
directory, or a packaged application.  

## Create an executable JAR file

A JAR file is a ZIP-based archive used to distribute Java classes and resources.  
An executable JAR contains a manifest that identifies the application's entry  
point.  

Create a file named `manifest.txt` in the project directory:  

```text
Manifest-Version: 1.0
Main-Class: com.example.Main

```

The blank line at the end of the manifest is required. `Main-Class` contains  
the fully qualified class name, including the package, but not `.class`.  

Create the JAR from the project directory:  

```text
jar --create --file bin/main.jar --manifest manifest.txt -C bin com/example/Main.class
```

The `-C bin` option changes to `bin` while adding the class. This keeps the  
package path inside the archive:  

```text
bin/
├── main.jar
└── com/
    └── example/
        └── Main.class
```

Run the executable JAR:  

```text
java -jar bin/main.jar
```

The `java` launcher reads `Main-Class` from the manifest and invokes that  
class's `main` method.  

## Clean and rebuild

Compiled classes can become stale after source code changes. Remove the output  
directory and compile again when you want a clean build:  

```text
rm -rf bin
mkdir -p bin
javac -d bin src/main/java/com/example/Main.java
```

On Windows PowerShell:  

```powershell
Remove-Item -Recurse -Force bin
New-Item -ItemType Directory bin
javac -d bin src\main\java\com\example\Main.java
```

## Common errors

**`javac: command not found`** means that a JDK is not installed or its `bin`  
directory is not on the `PATH`. Installing only a runtime is not enough to  
compile source code.  

**`Could not find or load main class`** usually means that the class path is  
wrong, the package name does not match the directory structure, or the class  
was not compiled. Compile again and use `-cp bin` from the project directory.  

**`Main-Class` errors when using `java -jar`** usually mean that the manifest  
contains a wrong class name or is missing its final newline. Use the fully  
qualified name `com.example.Main`.  
