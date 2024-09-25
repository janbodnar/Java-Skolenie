# Objects 

## Mutable & immutable objects

In Java, objects can be classified into two categories based on their mutability:  
*mutable* and *immutable*.

### Mutable Objects

Mutable objects can be modified after they are created. Their internal state can change over time.  

Examples:  
  - `ArrayList`
  - `StringBuilder`
  - Custom classes that have mutable fields

### Immutable Objects

Immutable objects cannot be modified once they are created. Their internal state remains constant  
throughout their lifetime.  

Examples:

- `String`
- `Integer`
- `Double`
- Custom classes designed to be immutable

**Why Immutability is Important:**

* **Thread Safety:** Immutable objects are inherently thread-safe. Multiple threads can safely share  
  and access an immutable object without the risk of data corruption.  
* **Caching:** Immutable objects can be cached more efficiently, as their values will never change.  
  This can improve performance in certain scenarios.  
* **Predictability:** Immutable objects are easier to reason about and predict their behavior, making  
  code more reliable and easier to maintain.  

**Creating Immutable Classes:**

To create an immutable class in Java:

1. **Declare all fields as final:** This prevents them from being modified after object creation.  
2. **Do not provide any public setters:** This ensures that the object's state cannot be changed from  
   outside.
4. **Make a defensive copy of mutable fields:** If the class contains mutable fields, create a defensive  
   copy (e.g., using `clone()` or `copyOf()`) when returning them from methods.  

By following these guidelines, we can create immutable classes in Java, which can enhance the  
reliability, thread safety, and performance of your applications.  



The following is a custom immutable object. 

```java
final class Point {

    private final int x;
    private final int y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public int getX() {
        return x;
    }

    public int getY() {
        return y;
    }
}

void main() {

    var p = new Point(4, 5);
    System.out.println(p);

    System.out.println(p.getX());
    System.out.println(p.getY());
}
```

## instanceof operator

The `instanceof` in Java is an operator used to check if an object is an instance of  
a particular class or interface. It returns a boolean value: `true` if the object  
is an instance of the specified type, and `false` otherwise.

```java

class Base {}
class Planet {}

void main() {

    List<Object> obs = List.of(new Base(), new Planet(), new Base(), new Planet(),
            new Base(), new Planet(), new Base(), new Base(), new Planet() );

    var r = new Random();

    for (int i = 0; i < 10; i++) {

        int idx = r.nextInt(obs.size());

        System.out.println(idx);
        var o = obs.get(idx);

        if (o instanceof Base) {
            System.out.println("Base");
        }

        if (o instanceof Planet) {
            System.out.println("Planet");
        }
    }
}
```

`instanceof` is often used in conjunction with downcasting to ensure type safety.  

```java
void main() {

    List<Shape> shapes = new ArrayList<>();
    shapes.add(new Circle(5));
    shapes.add(new Rectangle(4, 3));

    for (Shape shape : shapes) {
        if (shape instanceof Circle) {
            Circle circle = (Circle) shape;
            System.out.println("Circle area: " + circle.getArea());
        } else if (shape instanceof Rectangle) {
            Rectangle rectangle = (Rectangle) shape;
            System.out.println("Rectangle area: " + rectangle.getArea());
        } else {
            System.out.println("Unknown shape");
        }
    }
}


class Shape {
    // ...
}

class Circle extends Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    public double getArea() {
        return Math.PI * radius * radius;
    }
}

class Rectangle extends Shape {
    private double width;
    private double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    public double getArea() {
        return width * height;
    }
}
```


## Equals & hashCode

**equals**

- **Purpose:** Determines if two objects are equal in terms of their content or state.
- **Contract:**
  - Reflexive: `x.equals(x)` is always true.
  - Symmetric: If `x.equals(y)` is true, then `y.equals(x)` is also true.
  - Transitive: If `x.equals(y)` and `y.equals(z)` are true, then `x.equals(z)` is also true.
  - Consistent: Multiple invocations of `equals` on the same object with the same non-null  
    argument should produce the same result.
  - For any non-null reference `x`, `x.equals(null)` is always false.
- **Default implementation:** The default implementation in `Object` compares references.  
- Two objects are considered equal only if they are the same object.  
- **Custom implementation:** To define your own equality criteria, override the `equals` method  
  in your class. Consider comparing relevant fields using `==` for primitive types and `equals` for objects.  

**hashCode**

- **Purpose:** Returns a hash code value for an object. This value is used by data structures like `HashMap`  
  and `HashSet` to efficiently store and retrieve objects.
- **Contract:**
  - If two objects are equal according to `equals`, then their hash codes must be equal.
  - If two objects are not equal according to `equals`, their hash codes are not required to be different,  
    but it's generally recommended to have different hash codes for different objects to improve performance.  
- **Default implementation:** The default implementation in `Object` generates a hash code based on the  
  object's memory address.
- **Custom implementation:** To improve the efficiency of hash-based data structures, override the  
  `hashCode` method in your class. Consider using a combination of hash codes for relevant fields,  
   applying appropriate algorithms to avoid collisions.

**Relationship between `equals` and `hashCode`**

- If two objects are equal according to `equals`, their `hashCode` methods must return the same value.
- If two objects have different `hashCode` values, they are not equal according to `equals`. However, it's  
  possible for two non-equal objects to have the same `hashCode` (this is known as a hash collision).

**Best Practices**

- Always override both `equals` and `hashCode` together whenever you override one.
- Ensure that your `equals` implementation adheres to the contract.
- Choose a `hashCode` algorithm that minimizes collisions and provides a good distribution of hash values.  
- Consider using a library like Apache Commons Lang's `EqualsBuilder` and `HashCodeBuilder` to simplify  
  the implementation.

By following these guidelines, you can effectively implement `equals` and `hashCode` in your Java classes,  
ensuring correct object comparison and efficient use of hash-based data structures.

```java
import java.util.Objects;

class Person {

    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Person person = (Person) o;
        return Objects.equals(name, person.name) && age == person.age;
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }
}

void main() {

    Person p1 = new Person("John Doe", 32);
    Person p2 = new Person("John Doe", 32);

    System.out.println(p1.equals(p2));
    System.out.println(p1 == p2);
}
```




