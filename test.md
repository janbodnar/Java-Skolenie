# Priklady


## opakovanie

```java
import java.util.Arrays;

void main() {

    int[] vals = {1, 2, 3, 4, 5, 6};

    // calculate sum
    int sum = 0;

    for (int val : vals) {
        sum += val;
    }

    System.out.println("The sum is: " + sum);

    int sum2 = Arrays.stream(vals).sum();
    System.out.println(sum2);

    // print first and last element

    System.out.println(vals[0]);
    System.out.println(vals[vals.length - 1]);

    // iterate array from the end

    for (int i=vals.length-1; i >= 0 ; i--) {

        System.out.println(vals[i]);
    }
}
```




## Calculate sum from CSV file

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.List;

void main() throws IOException {

    String fileName = "data.csv";
    Path path = Path.of(fileName);

    List<String> lines = Files.readAllLines(path);

    int sum = 0;

    for (String line : lines) {

        String[] parts = line.split(",");

        for (String part: parts) {

            sum += Integer.parseInt(part); 
        }
    }

    System.out.println(sum);
}
```


## Circle/Rectangle

```java
package com.zetcode;


public class Main {

    public static void main(String[] args) {

        Circle c = new Circle(10);
        System.out.println(c.area());

        c.setRadius(5);
        System.out.println(c.area());

        c.setRadius(22);
        System.out.println(c.area());

        Rectangle r = new Rectangle(10, 20);
        System.out.println(r.getArea());
    }
}
```

```java
package com.zetcode;

public class Rectangle {

    private int width;
    private int height;

    public Rectangle(int width, int height) {
        this.width = width;
        this.height = height;
    }

    public int getWidth() {
        return width;
    }

    public void setWidth(int width) {
        this.width = width;
    }

    public int getHeight() {
        return height;
    }

    public void setHeight(int height) {
        this.height = height;
    }

    public int getArea() {

        return this.width * this.height;
    }

}
````

```java
package com.zetcode;

public class Circle {

    public Circle(int radius) {
        this.radius = radius;
    }

    private int radius;

    public void setRadius(int radius) {

        this.radius = radius;
    }

    public double area() {

        return this.radius * this.radius * Math.PI;
    }
}
```


## Getters/setters

```java
package com.zetcode;

class Person {

    private String firstName;
    private String lastName;

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
}

public class Main {

    public static void main(String[] args) {

        Person p1 = new Person();
        p1.setFirstName("Lucy");
        p1.setLastName("Black");

        Person p2 = new Person();
        p2.setFirstName("Maria");
        p2.setLastName("Novak");

        System.out.println(p1.getFirstName() + " " + p1.getLastName());
        System.out.println(p2.getFirstName() + " " + p2.getLastName());

    }
}
```


## Sum negative/positive values

```java
void main() {

    int[] vals = {1, -2, -4, 0, 5, 9, 11, -3};

    int sum_pos = 0;
    int sum_neg = 0;

    for (int val: vals) {

        if (val < 0) {
            sum_neg = sum_neg + val;
        }
        
        if (val > 0) {
            sum_pos = sum_pos + val;
        }
        
    }

    System.out.println(sum_neg);
    System.out.println(sum_pos);
}
```


## Read CSV data

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.List;

void main() throws IOException {

    String fileName = "data.csv";
    List<String> lines = Files.readAllLines(Path.of(fileName));

    int sum = 0;

    for (var line: lines) {

        String[] parts = line.split(",");

        for (String part: parts) {

            sum += Integer.parseInt(part);
        }

    }

    System.out.println(sum);
}
```


## Print words in titlecase

```java
void main() {

    String[] words = { "sky", "nord", "cup", "cloud", "war", "water" };

    for (String word: words) {

        System.out.println(Character.toUpperCase(word.charAt(0)) + word.substring(1).toLowerCase());
        
    }
}
```


## Generate 10 random integers

```java
import java.util.Random;

void main() {

    var random = new Random();

    for (var i = 0; i < 10; i++) {

        var r = random.nextInt(10);
        System.out.println(r);
    }
}
```


## Calculate sum

```java
void main() {

    int sum = 0;
    int[] vals = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

    for (int i = 0; i< vals.length; i++) {

        sum = sum + vals[i];
    }

    System.out.println(sum);
}
```

```java
void main() {

    int[] vals = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int sum = 0;

    for (int val: vals) {
        sum = sum + val;
    }

    System.out.println(sum);

    System.out.println("end of program");
}
```


## Formatovany vystup

```java
void main() {

    int age = 34;
    String name = "William";
    String occupation = "gardener";
    float weight = 78.5f;

    String output = String.format("%s is %d years old and he is a %s, his weight is %f kg", name, age, occupation, weight);
    System.out.println(output);
    
    System.out.printf("%s is %d years old and he is a %s, his weight is %f kg", name, age, occupation, weight);
}
```

## Premenne

```java
void main() {

    String name = "John Doe";
    int age = 34;

    System.out.println(name);
    System.out.println(age);

    name = "Roger Roe";
    System.out.println(name);

    age = 40;
    System.out.println(age);
}
```


```java
void main() {

    String name = "John Doe";
    int age = 34;
    String occupation = "gardener";

    System.out.println(name + " is " + age + " years old" + " and he is a " + occupation );
}
```
