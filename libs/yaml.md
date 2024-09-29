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

