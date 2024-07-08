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

## Plain JAR vs. Shadow Plugin in Gradle

The plain JAR plugin (built-in):

* This is the default Gradle task for creating a JAR archive.  
* It packages your compiled class files (*.class) and resources from your  
  project into a single JAR file.  
* *Dependencies:* It does not include any dependencies in the JAR. Your  
  application needs the libraries it depends on to be installed separately on  
  the target system.  
  
The shadow JAR plugin (external):  
  
* This is a popular third-party plugin for Gradle by John Engelman.   
* It creates a fat JAR or shadow JAR, which is a single JAR containing your  
  application code and all its transitive dependencies.  
* *Benefits:*  
    * *Simplified Deployment:* Makes deployment easier as you only need to  
      distribute the single JAR file containing everything your application  
      needs.  
    * *Reduced Startup Time:* Can potentially reduce the startup time of your  
      application since it doesn't need to locate and load individual  
      dependencies.  
* *Drawbacks:*  
    * *Larger JAR size:* The JAR file will be larger due to the inclusion of  
      all dependencies.  
    * *Potential Conflicts:* If your dependencies have conflicting classes,  
      the shadow plugin can resolve them by renaming packages (`relocation`).  
      This requires careful configuration.  

**Choosing Between Them:**

* Use the plain JAR plugin for simple projects where dependencies are managed  
  separately, like on a server environment with pre-installed libraries.  
* Use the shadow plugin for standalone applications or situations where managing  
  dependencies individually is cumbersome.   

Here's a table summarizing the key differences:

| Feature                 | Plain JAR Plugin             | Shadow Plugin              |
|--------------------------|------------------------------|----------------------------|
| Dependencies included    | No                           | Yes (transitively)           |
| File size               | Smaller                     | Larger                       |
| Deployment complexity    | More complex (manage deps)  | Simpler (single JAR)        |
| Startup time            | Potentially slower           | Potentially faster          |
| Dependency conflicts    | Not handled                  | Resolved by relocation (care needed) |


*With plain JAR plugin:*

This is the default Gradle task for creating a JAR archive. It packages your  
compiled class files (*.class) and resources from your project into a single JAR  
file.  

It does not include any dependencies in the JAR. Your application needs the  
libraries it depends on to be installed separately on the target system.  

```gradle
plugins {
    id 'java'
    id 'application'
}

group = 'com.zetcode'
version = '1.0-SNAPSHOT'

repositories {
    mavenCentral()
}

application {
    mainClass = 'com.zetcode.Main'
}

jar {
    duplicatesStrategy(DuplicatesStrategy.EXCLUDE)
    manifest {
        attributes(
                'Main-Class': 'com.zetcode.Main'
        )
    }
    from {
        configurations.runtimeClasspath.collect { it.isDirectory() ? it : zipTree(it) }
    }
}
```

## Executable JAR

*With shadow JAR plugin:*  

It creates a fat JAR or shadow JAR, which is a single JAR containing your  
application code and all its transitive dependencies.  

It makes deployment easier as you only need to distribute the single JAR file  
containing everything your application needs. The JAR file will be larger due to  
the inclusion of all dependencies.  


```gradle
plugins {
    id 'java'
    id 'application'
    id 'io.github.goooler.shadow' version '8.1.8'
}

group = 'com.zetcode'
version = '1.0-SNAPSHOT'

repositories {
    mavenCentral()
}

application {
    mainClass = 'com.zetcode.Main'
}

dependencies {
    implementation 'org.eclipse.collections:eclipse-collections:11.1.0'
}

jar {
//    duplicatesStrategy = DuplicatesStrategy.EXCLUDE
    duplicatesStrategy(DuplicatesStrategy.EXCLUDE)
    exclude 'META-INF/*.RSA', 'META-INF/*.SF', 'META-INF/*.DSA'
    manifest {
        attributes(
                'Main-Class': 'com.zetcode.Main'
        )
    }
    from {
        configurations.runtimeClasspath.collect { it.isDirectory() ? it : zipTree(it) }
    }
}
```
