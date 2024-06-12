# Definitions

## Java

Java is a high-level, general-purpose, object-oriented programming language. The  
main design goals of the language were robustness, portability, high performance  
and security. Java is a multithreaded and distributed programming language. It  
can be used to create console applications, GUI applications, web applications,  
both on PCs or embedded systems.  


Java is a programming language created by Sun Microsystems in 1991. The first  
publicly available version of Java was released in 1995. Today, the language is  
developed by Oracle corporation.  

Java excels in creating portable mobile applications, programming various  
appliances and in creating enterprise applications.  

![Java](images/java2.jpg)

## JVM

Java virtual machine (JVM) executes Java bytecode. The JVM is included in the  
JRE and JDK. Java source code is written in files with the .java extension. The  
javac Java compiler will compile the Java source code into the Java bytecode;  
the compiled files have the .class extension. This bytecode is executed by JVM.  
The java tool is a launcher for Java applications. Oracle's JVM is called  
HotSpot. HotSpot is a Java virtual machine for desktops and servers. It has  
advanced techniques such as just-in-time compilation and adaptive optimization  
designed to improve performance.  

## JRE

JRE (Java Runtime Environment) is a set of tools for executing Java  
applications. The JRE does not contain tools and utilities such as compilers or  
debuggers for developing Java applications.  

## JDK

JDK (Java Development Kit) is a superset of the JRE. It contains JRE and tools  
such as the compilers and debuggers necessary for developing Java applications.  
We need to install JDK to build and run our Java programs.  

## GraalVM

GraalVM is a high-performance JDK distribution designed to accelerate the  
execution of applications written in Java and other JVM languages⁵. It provides  
significant improvements in application performance and efficiency, making it  
ideal for microservices. 

Key features of GraalVM include:

- An alternative just-in-time (JIT) compiler that can speed up the performance of  
  Java and JVM-based applications.  
- A native image utility that compiles Java bytecode ahead-of-time (AOT) and generates  
  native executables for some applications. These executables start up almost  
  instantaneously and use very little memory resources.  
- Support for JavaScript, Ruby, Python, and a number of other popular languages.    
- Multilanguage interoperability through the Truffle language implementation framework.   

GraalVM started in 2011 as a research project at Oracle Labs to create a runtime platform  
that can run multiple programming languages with high performance.  

