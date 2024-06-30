# Compile & run 

```
mkdir bin
mkdir src\main\java\com\zetcode
```


```
src
└───main
    └───java
        └───com
            └───example
                    Main.java
```

```java
package com.example;

public class Main {

    public static void main(String... args) {

        System.out.println("hello there!");
    }
}
```

## Compile 

Compile source code into Java bytecode with `javac`. The bytecode is placed  
into the `bin` directory.  

```
javac -d bin src\main\java\com\example\Main.java
```

## Run 

Run the code with the `java` tool.  

```
java -cp bin com.example.Main
```

Specify the location of the bytecode with `-cp` option. Provide the full name  
of the program `com.example.Main` without the `.class` suffix.  

## Java runner

It is possible to run small Java programs directly with `java` from the source  
code.  

```
java src\main\java\com\example\Main.java
```

The tool simply compiles and runs the program in one step.  

## Create executable JAR file 

`cd bin`

Go inside the `bin` directory. 

```
Manifest-Version: 1.0
Main-Class: com.example.Main

```

In the manifest file, we provide the path to the main function of the program.  
Note that the file *must be* ended in a new line, otherwise it will not work.  

```
jar -cvfm main.jar manifest.txt com
```

Create the executable JAR file with the `jar` command. 

```
bin
│   main.jar
│   manifest.txt
│
└───com
    └───example
            Main.class
```


```
java -jar main.jar
```

Run the JAR file.  
