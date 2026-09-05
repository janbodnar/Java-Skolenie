# Introduction to Java

Java is a general-purpose programming language used to build applications for  
desktops, servers, mobile devices, embedded systems, and the web. It was  
designed to be readable, reliable, and portable. Java is a good language for  
learning programming because its syntax is explicit and its standard library  
contains tools for many common tasks.  

## A short history of Java

Java began at Sun Microsystems in 1991 as part of the Green project. The  
language was originally called Oak and was designed for consumer electronic  
devices. It was renamed Java and publicly released in 1995. Its promise of  
"write once, run anywhere" helped it become popular for programs that needed to  
run on many different operating systems.  

The first Java Development Kit (JDK 1.0) was released in 1996. Java later  
became an important language for web applications, enterprise software, mobile  
devices, and server-side systems. Oracle acquired Sun Microsystems in 2010 and  
continues to develop the Java platform. Since 2017, new Java feature releases  
have generally followed a six-month release cycle, with regular long-term  
support (LTS) releases intended for applications that need a longer maintenance  
period.  

## Key terms

The following terms describe the Java development and execution environment.  

### Java source code

Java source code is the human-readable code written by a programmer. Source  
files normally use the `.java` extension. For example, a file named  
`Hello.java` can contain a Java program.  

### Bytecode and class files

The `javac` Java compiler translates Java source code into Java bytecode. The  
compiled bytecode is normally stored in files with the `.class` extension. It  
is not machine code for one particular operating system; it is an intermediate  
format designed to be executed by a JVM.  

### Java Virtual Machine (JVM)

The Java Virtual Machine executes Java bytecode. A JVM is available for many  
operating systems and hardware platforms, which is the main reason Java  
programs are portable. The JVM also provides memory management, garbage  
collection, security features, and runtime checks.  

The `java` tool is a launcher for Java applications. It starts a JVM and asks it  
to execute a class or a source file. The exact JVM implementation depends on  
the installed Java distribution and operating system.  

### Java Runtime Environment (JRE)

The Java Runtime Environment is the part of the Java platform needed to run  
Java applications. Conceptually, it contains a JVM and the Java class libraries,  
but it does not contain development tools such as the Java compiler or  
debuggers.  

Older Java distributions were commonly described as separate JRE and JDK  
installations. Since Java 9, most vendors distribute a JDK that already  
contains the runtime components, rather than a separate downloadable JRE. The  
JRE remains useful as a conceptual term for the runtime portion of Java.  

### Java Development Kit (JDK)

The Java Development Kit is the complete toolkit for developing Java  
applications. It contains the runtime components, including a JVM and standard  
libraries, together with tools such as:  

- `javac`, the Java compiler;
- `java`, the application launcher;
- `javadoc`, the documentation generator;
- `jdb`, the Java debugger;
- `jar`, the tool for creating Java archives.

We install a JDK to compile and run the programs in this course. A useful  
relationship between the terms is:  

```text
JDK = runtime environment + development tools
runtime environment = JVM + standard libraries
```

### HotSpot

HotSpot is a JVM implementation originally developed at Sun Microsystems and  
now maintained by Oracle. It is used for desktop, server, and other general  
purpose applications. HotSpot improves performance with **just-in-time (JIT)  
compilation**, which compiles frequently executed bytecode into native machine  
code while the program is running. It also uses **adaptive optimization** to  
adjust its decisions according to the program's actual behavior.  

HotSpot is one JVM implementation, not a different Java language. Other JVM  
implementations can execute the same Java bytecode when they conform to the  
Java platform specification.  

### OpenJDK

OpenJDK is the open-source reference implementation of the Java platform. It  
contains the source code for the Java Development Kit and is developed by a  
community that includes Oracle and other organizations. Many vendors build  
their Java distributions from OpenJDK, adding support, installers, or other  
distribution-specific changes.  

Examples of OpenJDK-based distributions include Oracle JDK, Eclipse Temurin,  
Amazon Corretto, Microsoft Build of OpenJDK, and Azul Zulu. For learning Java,  
any current JDK that supports the examples in this course is usually suitable.  

## Why Java is portable

Java source code is compiled into **bytecode**. Bytecode is stored in `.class`  
files and is executed by the Java Virtual Machine (JVM). A JVM is available for  
many operating systems, so the same compiled program can run on different  
systems.  

The usual process looks like this:  

```text
Java source code -> Java compiler -> bytecode -> JVM -> program output
```

The JVM also manages memory and provides automatic garbage collection. This  
means that Java programs usually do not need to release objects manually after  
they are no longer used.  

## A first Java program

Modern Java supports an implicit class for small programs. This keeps the first  
example focused on the program itself:  

```java
void main() {
		System.out.println("Hello, Java!");
}
```

The `main` method is the entry point of the program. Execution starts with the  
statements inside its body. Curly brackets `{}` mark the beginning and end of  
the method body, and the semicolon terminates a statement.  

`System.out.println` writes text to the standard output and then starts a new  
line. The text between double quotes is a string literal.  

The program can be run directly from a file with a recent JDK:  

```text
java Hello.java
```

For larger applications, Java code is usually organized into classes and  
packages. The implicit-class form is useful for short examples and learning;  
the course will also introduce the explicit class form used in many production  
projects.  

## What makes Java different

Java has several important characteristics:  

- **Statically typed:** every variable has a type, such as `int`, `double`, or
	`String`. Many errors can therefore be found before the program runs.  
- **Object-oriented:** programs can be organized around objects that contain
	data and behavior.  
- **Garbage-collected:** the runtime automatically reclaims memory that is no
	longer needed.  
- **Multithreaded:** the standard library provides tools for running tasks
	concurrently.  
- **Strong standard library:** Java includes APIs for collections, files,
	networking, dates, regular expressions, databases, and more.  
- **Backward compatible:** Java evolves regularly while maintaining a strong
	focus on compatibility with existing applications.  

## The basic building blocks

During the course, Java programs will be built from these elements:  

1. **Values and variables** store information.
2. **Expressions and operators** calculate new values.
3. **Statements** perform actions.
4. **Conditions and loops** control which statements are executed and how often.
5. **Methods** group reusable operations.
6. **Classes and objects** model data and behavior.
7. **Collections** store groups of values.
8. **Exceptions** represent and handle errors.
9. **Streams and lambdas** allow concise processing of data.
10. **Packages and libraries** organize and extend a program.

For example, the following program declares a variable, calls a method, and  
prints the result:  

```java
void main() {
    var language = "Java";
    var message = "Learning " + language;

    System.out.println(message);
}
```

The `var` keyword lets the compiler infer the type from the value on the right  
side. The variable still has a fixed type; `var` does not make Java dynamically  
typed.  

## How to use this course

The topics in this course build on one another. Start with expressions,  
variables, and control flow. Then continue with methods, classes, collections,  
exceptions, input and output, and streams. Later sections cover databases,  
user interfaces, concurrency, and external libraries.  

For each example:  

1. Read the code and identify its variables, methods, and control flow.
2. Run the example.
3. Change one part of it and observe the result.
4. Try to explain the result before running the program again.

Programming is learned by writing and changing programs. The examples are  
starting points for experiments, not only text to read.  
