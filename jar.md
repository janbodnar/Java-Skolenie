# JAR

JAR stands for *Java ARchive*. It's a file format used to aggregate many  
files, primarily  *.class* files (compiled Java code), and other resources  
(text files, images, etc.) into a single archive. 

JAR characteristics:  

* *Structure:* JAR files can contain a manifest file (META-INF/MANIFEST.MF)  
  that provides metadata about the archive, such as the main class to run or  
  dependencies on other JARs.  
* *Platform-independent:* JAR files are platform-independent, meaning they can  
  be run on any system with a Java Runtime Environment (JRE) installed.  
* *Designed for Java applications:* JARs are specifically designed for  
  packaging and distributing Java applications, libraries, and applets.  


* *Distribution:* JARs provide a convenient way to distribute entire Java  
  applications or libraries in a single file. This simplifies deployment and  
  reduces the risk of missing files.  
* *Classpath management:* JARs can be added to the classpath, which is a list of  
  locations where the Java runtime searches for classes and resources. This  
  allows applications to access classes and resources stored within JARs.  
* *Modularization:* JARs can be used to package reusable components like  
  libraries or frameworks. This promotes modularity and code organization.  

Here are some common types of JAR files:

* *Executable JARs:* These JARs contain a manifest file that specifies the main  
  class to run. They can be executed directly from the command line using the  
  `java -jar` command.  
* *Library JARs:* These JARs contain only class files and are meant to be used  
  by other applications. They don't have a main class and cannot be executed  
  directly.  

## Create JAR in IntelliJ IDEA

- Project structure
- Artifacts
- Add JAR / From modules with dependencies
- Create manifest file with path to main method
- Build / Build Artifacts

## Create JAR with Maven 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.zetcode</groupId>
    <artifactId>ExecutableJar</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>22</maven.compiler.source>
        <maven.compiler.target>22</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>3.6.0</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                        <configuration>a
                            <transformers>
                                <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                                    <manifestEntries>
                                        <Main-Class>com.zetcode.Main</Main-Class>
                                        <Build-Number>1.0</Build-Number>
                                    </manifestEntries>
                                </transformer>
                            </transformers>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

</project>
```

