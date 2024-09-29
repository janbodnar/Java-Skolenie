# YAML

**YAML** (YAML Ain't Markup Language) is a human-readable data-serialization language. It is often  
used for configuration files, data interchange, and storing structured data. 

## Key characteristics of YAML:

* **Human-readable:** YAML syntax is designed to be easily understood by humans, making it  
  a good choice for configuration files and data interchange.  
* **Flexible:** YAML supports a variety of data types, including scalars, sequences,  
  mappings, and even custom types.  
* **Compact:** YAML syntax is often more concise than XML or JSON, making it suitable  
  for storing large amounts of data.  
* **Versatile:** YAML can be used for a wide range of applications, from simple configuration  
  files to complex data structures.  

## Basic YAML syntax:

* **Scalars:** Simple values, such as strings, numbers, booleans, or null.
  ```yaml
  name: John Doe
  age: 30
  is_active: true
  ```
* **Sequences:** Ordered lists of values.
  ```yaml
  fruits:
    - apple
    - banana
    - orange
  ```
* **Mappings:** Key-value pairs.
  ```yaml
  person:
    name: Alice
    age: 25
    address:
      street: Main Street
      city: New York
  ```


YAML is commonly used in various contexts:

* **Configuration files:** For storing settings and preferences for applications.
* **Data interchange:** For exchanging data between different systems.
* **Serialization:** For storing and retrieving structured data.
* **Automation tools:** For defining tasks and workflows.

Overall, YAML is a versatile and easy-to-use language that is well-suited for a variety of data-related tasks.


`Snakeyaml` is a YAML parser and emitter for Java. It provides a simple API for reading and  
writing YAML data structures. Snakeyaml is a popular choice for Java developers working with  
YAML files due to its ease of use and performance.


## Simple example

`data.yaml`

```yaml
name: John Doe
age: 34
height: 185.5
kids: [Paul, Marta, Simon]
```

`Main.java`

```java
import org.yaml.snakeyaml.Yaml;

void main() throws IOException {

    Yaml yaml = new Yaml();
    String fileName = "src/main/resources/data.yaml";

    try (var fr = new FileReader(fileName, StandardCharsets.UTF_8)) {

        Map<String, Object> res = yaml.load(fr);
        String name = (String) res.get("name");
        int age = (int) res.get("age");
        double height = (double) res.get("height");

        System.out.println(name);
        System.out.println(age);
        System.out.println(height);
        
//        List<?> ko = (List<?>) res.get("kids");
        @SuppressWarnings(value = "unchecked")
        List<String> ko = (List<String>) res.get("kids");
        System.out.println(ko);

    }
}
```

## Reading a list of users 

`users.yaml`

```yaml
firstName: John
lastName: Doe
occupation: gardener
---
firstName: Roger
lastName: Roe
occupation: driver
---
firstName: Peter
lastName: Novak
occupation: programmer
```

`User.java`

The Java class into which we read the data must be a regular class with a  
default constructor.  

```java
package com.zetcode;

import java.util.Objects;

public class User {
    private String firstName;
    private String lastName;
    private String occupation;

    public User() {

    }

    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    public String getOccupation() {
        return occupation;
    }

    public void setOccupation(String occupation) {
        this.occupation = occupation;
    }

    @Override
    public final boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof User user)) return false;

        return Objects.equals(firstName, user.firstName)
                && Objects.equals(lastName, user.lastName)
                && Objects.equals(occupation, user.occupation);
    }

    @Override
    public int hashCode() {
        int result = Objects.hashCode(firstName);
        result = 31 * result + Objects.hashCode(lastName);
        result = 31 * result + Objects.hashCode(occupation);
        return result;
    }

    @Override
    public String toString() {
        final StringBuilder sb = new StringBuilder("User{");
        sb.append("firstName='").append(firstName).append('\'');
        sb.append(", lastName='").append(lastName).append('\'');
        sb.append(", occupation='").append(occupation).append('\'');
        sb.append('}');
        return sb.toString();
    }
}
```

`Main.java`

```java
import com.zetcode.User;
import org.yaml.snakeyaml.LoaderOptions;
import org.yaml.snakeyaml.constructor.Constructor;
import org.yaml.snakeyaml.Yaml;

void main() throws IOException {

    Yaml yaml = new Yaml(new Constructor(User.class, new LoaderOptions()));
    String fileName = "src/main/resources/users.yaml";

    try (var fr = new FileReader(fileName, StandardCharsets.UTF_8)) {

        var res = yaml.loadAll(fr);
        res.forEach(System.out::println);
    }
}
```

The `loadAll` method oarses all YAML documents in the `Reader` and produce corresponding Java objects.  


## Writing data

`User.java`

```java
package com.zetcode;

import java.util.Objects;

public class User {
    private String firstName;
    private String lastName;
    private String occupation;

    public User(String firstName, String lastName, String occupation) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.occupation = occupation;
    }

    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    public String getOccupation() {
        return occupation;
    }

    public void setOccupation(String occupation) {
        this.occupation = occupation;
    }

    @Override
    public final boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof User user)) return false;

        return Objects.equals(firstName, user.firstName)
                && Objects.equals(lastName, user.lastName)
                && Objects.equals(occupation, user.occupation);
    }

    @Override
    public int hashCode() {
        int result = Objects.hashCode(firstName);
        result = 31 * result + Objects.hashCode(lastName);
        result = 31 * result + Objects.hashCode(occupation);
        return result;
    }

    @Override
    public String toString() {
        final StringBuilder sb = new StringBuilder("User{");
        sb.append("firstName='").append(firstName).append('\'');
        sb.append(", lastName='").append(lastName).append('\'');
        sb.append(", occupation='").append(occupation).append('\'');
        sb.append('}');
        return sb.toString();
    }
}
```

`Main.java`

```java
import com.zetcode.User;
import org.yaml.snakeyaml.DumperOptions;
import org.yaml.snakeyaml.Yaml;

void main() throws IOException {

    var dops = new DumperOptions();
    dops.setIndent(2);


    Yaml yaml = new Yaml(dops);
    String fileName = "src/main/resources/users2.yaml";

    var users = List.of(new User("John", "Doe", "gardener"),
            new User("Roger", "Roe", "driver"),
            new User("Peter", "Novak", "programmer")
    );
    
    try (var wr = new FileWriter(fileName, StandardCharsets.UTF_8)) {

        yaml.dump(users, wr);
    }
}
```


