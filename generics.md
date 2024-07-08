# Generics

Java generics allows us to write code that can work with a variety of data  
types. Before generics, programmers had to create separate classes or methods  
for each data type they wanted to work with. This could lead to a lot of  
repetitive code.  

Generics address this problem by introducing the concept of *type parameters*.  
These placeholders are like variables that can be replaced with specific data  
types when the code is used. This allows us to write a single class or method  
that can be used with many different data types.  

Here are some of the key benefits of using generics in Java:  

* *Improved code reusability:* We can write generic code that can be used  
  with different data types, reducing the need to duplicate code.  
* *Enhanced type safety:* Generics help to prevent errors at compile time by  
  ensuring that the data types used with a generic class or method are  
  compatible.  
* *More readable code:* Generic code can be more readable and easier to  
  understand, as it is clear what types of data the code can work with.  

Here are some of the common types of Java generics:  

* *Generic classes:* These classes use type parameters to specify the type of  
  data that they can hold. For example, an `ArrayList<String>` can hold a list  
  of strings, while an `ArrayList<Integer>` can hold a list of integers.  
* *Generic methods:* These methods use type parameters to specify the types of  
  the arguments they can accept and the type of the value they return. For  
  example, a `sort` method might be generic, allowing it to sort arrays of  
  different data types.  


## Raw list

In Java, raw lists refer to lists created without specifying a type argument for  
generics. Before generics were introduced in Java 5, all lists were essentially  
raw lists.   

Here's a breakdown of raw lists:

* *Generics:* Introduced in Java 5, generics allow you to define types for  
  collections like lists, ensuring type safety and code clarity.  
* *Raw Lists:* These lists lack type information and are simply declared as  
  `List`.  


The usage of raw lists is discouraged:  

* *Lack of Type Safety:* The biggest issue is the lack of type safety. The  
  compiler can't enforce type checks, potentially leading to runtime errors like  
  `ClassCastException`.  
* *Less Readable Code:* Without type information, the code becomes less  
  readable. It's not clear what types of elements the list can hold.  
* *Limited Functionality:* Some generic methods and features might not work with  
  raw lists.

While technically possible, using raw lists is generally discouraged in favor of  
generics. Generics provide type safety, improve code readability, and offer more  
functionalities.  


```java
import java.util.ArrayList;
import java.util.List;

class Base {
}

void main() {

    List da = new ArrayList();

    da.add("Java");
    da.add(3.5);
    da.add(55);
    da.add(new Base());

    for (Object el : da) {
        System.out.println(el);
    }
}
```

The type for the list is `List<Object>`. In Java, when we declare a list  
without specifying a type, it defaults to a raw type, which allows we to add  
elements of any type. In the example, the list `da` can hold objects of  
different types, including strings, doubles, integers, and instances of the  
`Base` class. 

However, using raw types is discouraged because it lacks type safety. It's  
better to specify the type explicitly, such as `List<String>` or  
`List<Integer>`, to ensure type correctness and avoid runtime errors.  


It is better to always explicitly set the type for the list.  

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    List<String> langs = new ArrayList<>();
    langs.add("Java");
    langs.add("C#");
    langs.add("Ruby");

    List<Integer> vals = new ArrayList<>();
    vals.add(55);
    vals.add(45);
    vals.add(33);

    List<Float> weights = new ArrayList<>();
    weights.add(3.5f);
    weights.add(5.5f);

    langs.forEach(System.out::println);
    vals.forEach(System.out::println);
    weights.forEach(System.out::println);
}
```




## Generic method

The following example defines a method that returns a random value from a list. 

```java
import java.util.List;
import java.util.Random;


void main() {

    var words = List.of("rock", "sky", "blue", "ocean", "falcon");
    var vals = List.of(2, 3, 4, 5, 6, 7, 8);

    var e1 = getRandomElement(words);
    System.out.println(e1);

    var e2 = getRandomElement(vals);
    System.out.println(e2);
}

<T> T getRandomElement(List<T> list) {

    var random = new Random();
    int idx = random.nextInt(list.size());
    return list.get(idx);
}
```

Single definition of `getRandomElement` can be used for both integers or strings.


```java
<T> T getRandomElement(List<T> list) {
...
}
```

The `<T>` is used to declare the method as generic. The `T` represents a
placeholder for any data type. The `T getRandomElement(List<T> list)` syntax
defines the method name (`getRandomElement`), the parameter it takes 
(`List<T> list`), and the return type (`T`).



## Generic forEach method

The following example creates a generic `forEach` method.

```java
import java.util.List;
import java.util.function.Consumer;


void main() {

    var data = List.of(1, 2, 3, 4, 5, 6, 7);

//      Consumer<Integer> consumer = (Integer x) ->  System.out.println(x);
    Consumer<Integer> consumer = System.out::println;
    forEach(data, consumer);

    System.out.println("--------------------------");

    forEach(data, System.out::println);

    System.out.println("--------------------------");

    var words = List.of("sky", "town", "brown", "pen", "forest");
    forEach(words, System.out::println);
}

<T> void forEach(List<T> data, Consumer<T> consumer) {

    for (T t : data) {
        consumer.accept(t);
    }
}
```

## Generic concatenate method

The example creates a generic concatenate method that adds joins multiple lists.  


```java
import java.util.ArrayList;
import java.util.List;


void main() {

    var vals1 = List.of(1, 2, 3);
    var vals2 = List.of(4, 5, 6);
    var vals3 = List.of(7, 8, 9);

    var vals = concatenate(vals1, vals2, vals3);

    System.out.println(vals);

    var words1 = List.of("pen", "paper", "ink");
    var words2 = List.of("sky", "cloud", "wind");
    var words3 = List.of("tree", "forest", "wood");

    var words = concatenate(words1, words2, words3);

    System.out.println(words);
}

@SafeVarargs
final <T> List<T> concatenate(List<T>... lists) {
    return new ArrayList<>() {{

        for (List<T> mylist : lists) {

            addAll(mylist);
        }
    }};
}
```

In the example, using `final` protects the core functionality and `@SafeVarargs`  
ensures type safety when dealing with variable arguments.  

## Bounded generics

Bounded generics in Java are a way to restrict the types that can be used as a  
generic parameter in a class, interface, or method. By setting bounds, you  
ensure the generic code can only work with types that inherit specific  
functionalities or belong to a specific category.  

Generics allow us to write code that works with various data types using  
placeholders like `<T>`. Bounds are limitations that define what types can be  
used in place of the generic placeholder.  

```java
interface Item {

    String info();
}

interface Plant {

    String getColor();
}

class Bike implements Item {

    @Override
    public String info() {

        return "This is a bike";
    }
}

class Chair implements Item {

    @Override
    public String info() {

        return "This is a chair";
    }
}

class Flower implements Item, Plant {

    private String color;

    public Flower(String color) {
        this.color = color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    @Override
    public String getColor() {
        return this.color;
    }

    @Override
    public String info() {

        return String.format("This is %s flower", this.color);
    }
}

// Generic bounded example


void main(String[] args) {

    var chair = new Chair();
    doInform2(chair);

    var flower = new Flower("red");
    doInform(flower);
}

<T extends Item & Plant> void doInform(T item) {

    System.out.println(item.info());
}

<T extends Item> void doInform2(T item) {

    System.out.println(item.info());
}
```

In the example, the `doInform` method uses a bounded type parameter. The item  
that it taks must implement both `Item` and `Plant` interfaces.  


The `<T extends Item & Plant>` syntax is a generic type parameter. It means that  
the method `doInform` can accept any type T that extends both Item and Plant. In  
other words, T must be a subtype of both Item and Plant.  


## Generic wildcard 

A wildcard is a way to represent unknown types with some restrictions. It allows  
more flexibility when working with generic collections but with some limitations  
compared to specific types.  

While generics allow us to write code that works with various data types using  
placeholders like `<T>`, wildcards (`?`) symbol represents an unknown type.  

The key difference between `? extends Shape` and `T extends Shape` in Java  
generics lies in the level of specificity and mutability they offer: 

Here's a table summarizing the key differences:

| Feature                 | `? extends Shape` (Wildcard) | `T extends Shape` (Generic Type) |
|--------------------------|---------------------------------|------------------------------------|
| Specificity              | Unknown subtype of Shape         | Specific subclass of Shape          |
| Flexibility              | More flexible, works with various subtypes  | Less flexible, requires specific type |
| Mutability (Reading)     | Allowed                          | Allowed                          |
| Mutability (Adding)      | Not Allowed (unsafe)             | Allowed (type safety enforced)    |



```java
import java.util.ArrayList;
import java.util.List;

abstract class Shape {

    abstract void draw();
}

class Rectangle extends Shape {

    @Override
    void draw() {
        System.out.println("Drawing rectangle");
    }
}

class Circle extends Shape {

    @Override
    void draw() {
        System.out.println("Drawing circle");
    }
}

// Generic wildcard example

void main(String[] args) {

    List<Rectangle> list1 = new ArrayList<>();
    list1.add(new Rectangle());

    List<Circle> list2 = new ArrayList<>();
    list2.add(new Circle());
    list2.add(new Circle());

    List<Shape> list3 = new ArrayList<>();
    list3.add(new Circle());
    list3.add(new Rectangle());

    drawShapes(list1);
    drawShapes(list2);
    drawShapes(list3);
}

void drawShapes(List<? extends Shape> lists) {

    for (Shape s : lists) {
        s.draw();
    }
}
```
