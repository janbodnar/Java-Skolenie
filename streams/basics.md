# Streams

A stream is a sequence of elements from a source that supports sequential and  
parallel aggregate operations. The common aggregate operations are: filter, map,  
reduce, find, match, and sort. The source can be a collection, IO operation, or  
array, which provides data to a stream. 

A Java collection is an in-memory data structure with all elements contained  
within memory while a stream is a data structure with all elements computed on  
demand. In contrast to collections, which are iterated explicitly (external  
iteration), stream operations do the iteration behind the scenes for us. Since  
Java 8, Java collections have a stream method that returns a stream from a  
collection.  

The Stream interface is defined in `java.util.stream` package.  

An operation on a stream produces a result without modifying its source. 

Characteristics of a stream

- Streams do not store data; rather, they provide data from a source such as a  
  collection, array, or IO channel.  
- Streams do no modify the data source. They transform data into a new stream,  
  for instance, when doing a filtering operation.  
- Many stream operations are lazily-evaluated. This allows for automatic code  
  optimizations and short-circuit evaluation.  
- Stream can be infinite. Method such as limit allow us to get some result from  
  infinite streams.  
- The elements of a stream can be reached only once during the life of a stream.  
  Like an Iterator, a new stream must be generated to revisit the same elements  
  of the source.  
- Streams have methods, such as `forEach` and `forEachOrdered`, for internal  
  iteration of stream elements.  
- Streams support SQL-like operations and common functional operations, such as  
  filter, map, reduce, find, match, and sorted.  

## Stream pipeline

A stream pipeline consists of a source, intermediate operations, and a terminal  
operation. Intermediate operations return a new modified stream; therefore, it  
is possible to chain multiple intermediate operations. Terminal operations, on  
the other hand, return void or a value. After a terminal operation it is not  
possible to work with the stream anymore. Short-circuiting a terminal operation  
means that the stream may terminate before all values are processed. This is  
useful if the stream is infinite.  

Intermediate operations are lazy. They will not be invoked until the terminal  
operation is executed. This improves the performance when we are processing  
larger data streams.  

## Creating streams

Streams are created from various sources such as collections, arrays, strings,  
IO resources, or generators.  

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.IntStream;
import java.util.stream.Stream;

void main() {

    List<String> words = List.of("pen", "coin", "desk", "chair");

    String word = words.stream().findFirst().get();
    System.out.println(word);

    Stream<String> letters = Arrays.stream(new String[]{"a", "b", "c"});
    System.out.printf("There are %d letters%n", letters.count());

    String day = "Sunday";
    IntStream istr = day.codePoints();

    String s = istr.filter(e -> e != 'n').collect(StringBuilder::new,
            StringBuilder::appendCodePoint, StringBuilder::append).toString();
    System.out.println(s);
}
```

In this example, we work with streams created from a list, array, and a string.  

```java
List<String> words = List.of("pen", "coin", "desk", "chair");
```

A list of strings is created.

```java
String word = words.stream().findFirst().get();
```

With the stream method, we create a stream from a list collection. On the  
stream, we call the findFirst method which returns the first element of the  
stream. (It returns an `Optional` from which we fetch the value with the get  
method.)  

```java
Stream<String> letters = Arrays.stream(new String[]{ "a", "b", "c"});
```

```java
System.out.printf("There are %d letters%n", letters.count());
```

We create a stream from an array. The count method of the stream returns the  
number of elements in the stream.  

```java
String day = "Sunday";
IntStream istr = day.codePoints();

String s = istr.filter(e -> e != 'n').collect(StringBuilder::new,
        StringBuilder::appendCodePoint, StringBuilder::append).toString();
System.out.println(s);
```

Here we create a stream from a string. We filter the characters and build a new  
string from the filtered characters.  

There are three `Stream` specializations: `IntStream`, `DoubleStream`,  
and `LongStream`.  

```java
import java.util.stream.DoubleStream;
import java.util.stream.IntStream;
import java.util.stream.LongStream;

    void main() {

        IntStream integers = IntStream.rangeClosed(1, 16);
        System.out.println(integers.average().getAsDouble());

        DoubleStream doubles = DoubleStream.of(2.3, 33.1, 45.3);
        doubles.forEachOrdered(e -> System.out.println(e));

        LongStream longs = LongStream.range(6, 25);
        System.out.println(longs.count());
    }
```

The example works with the three aforementioned specializations.  

```java
IntStream integers = IntStream.rangeClosed(1, 16);
System.out.println(integers.average().getAsDouble());
```

A stream of integers is created with the `IntStream.rangeClosed` method. We  
print their average to the console.  

```java
DoubleStream doubles = DoubleStream.of(2.3, 33.1, 45.3);
doubles.forEachOrdered(e -> System.out.println(e));
```

A stream of double values is created with the `DoubleStream.of` method. We print  
the ordered list of elements to the console utilizing the `forEachOrdered`  
method.  

```java
LongStream longs = LongStream.range(6, 25);
System.out.println(longs.count());
```

A stream of long integers is created with the `LongStream.range` method. We  
print the count of the elements with the `count` method.  


The `Stream.of` method returns a sequential ordered stream whose elements are  
the specified values.  

```java
import java.util.Comparator;
import java.util.stream.Stream;

    void main() {

        Stream<String> colours = Stream.of("red", "green", "blue");
        String col = colours.skip(2).findFirst().get();
        System.out.println(col);

        Stream<Integer> nums = Stream.of(3, 4, 5, 6, 7);
        int maxVal = nums.max(Comparator.naturalOrder()).get();
        System.out.println(maxVal);
    }
```

In the example, we create two streams with the `Stream.of` method.  

```java
Stream<String> colours = Stream.of("red", "green", "blue");
```

A stream of three strings is created.  

```java
String col = colours.skip(2).findFirst().get();
```

With the `skip` method, we skip two elements and find the only one left with the  
`findFirst` method.

```java
Stream<Integer> nums = Stream.of(3, 4, 5, 6, 7);
int maxVal = nums.max(Comparator.naturalOrder()).get();
```

We create a stream of integers and find its maximum number.  


Other methods to create streams are: `Stream.iterate` and `Stream.generate`.  

```java
import java.util.Random;
import java.util.stream.Stream;

void main() {

    Stream<Integer> s1 = Stream.iterate(5, n -> n * 2).limit(10);
    s1.forEach(System.out::println);

    Stream.generate(new Random()::nextDouble)
            .map(e -> (e * 10))
            .limit(5)
            .forEach(System.out::println);
}
```

In the example, we create two streams with `Stream.iterate` and `Stream.generate`.

```java
Stream<Integer> s1 = Stream.iterate(5, n -> n * 2).limit(10);
s1.forEach(System.out::println);
```

The `Stream.iterate` returns an infinite sequential ordered stream produced by  
iterative application of a function to an initial element. The initial element  
is called a seed. The second element is generated by applying the function to  
the first element. The third element is generated by applying the function on  
the second element etc.  

```java
Stream.generate(new Random()::nextDouble)
        .map(e -> (e * 10))
        .limit(5)
        .forEach(System.out::println);
```

A stream of five random doubles is created with the `Stream.generate` method.  
Each of the elements is multiplied by ten. In the end, we iterate over the  
stream and print each element to the console.  


It is possible to create a stream from a file.  

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.stream.Stream;

void main() throws IOException {

    Path path = Paths.get("/home/janbodnar/myfile.txt");
    Stream<String> stream = Files.lines(path);

    stream.forEach(System.out::println);
}
```

The example reads a file and prints its contents using streams.  

```java
Path path = Paths.get("/home/janbodnar/myfile.txt");
```

A `Path` object is created with `Paths.get` method. A `Path` object is used to  
locate a file in a file system.  

```java
Stream<String> stream = Files.lines(path);
```

From the path, we create a stream using `Files.lines` method; each of the  
elements of the stream is a line.  

```java
stream.forEach(System.out::println);
```

We go through the elements of the stream and print them to the console.


## Internal and external iteration

Depending on who controls the iteration process, we distinguish between external  
and internal iteration. External iteration, also known as active or explicit  
iteration, is handled by the programmer. Until Java 8, it was the only type of  
iteration in Java. For external iteration, we use for and while loops. Internal  
iteration, also called passive or implicit iteration, is controlled by the  
iterator itself. Internal iteration is available in Java streams.  

```java
import java.util.Iterator;
import java.util.List;

void main() {

    var words = List.of("pen", "coin", "desk", "eye", "bottle");

    Iterator<String> it = words.iterator();

    while (it.hasNext()) {

        System.out.println(it.next());
    }
}
```

In the code example, we retrieve and iterator object from a list of strings.  
Using iterator's `hasNext` and next method in a while loop, we iterate over the  
elements of the list.  

In the following example, we iterate the same list using an external iteration.  

```java
import java.util.List;

void main() {

    var words = List.of("pen", "coin", "desk", "eye", "bottle");

    words.stream().forEach(System.out::println);
}
```

In the example, we create a stream from a list. We use the stream's `forEach`  
to internally iterate over the stream elements.

```java
words.stream().forEach(System.out::println);
```

This can be shortened to `words.forEach(System.out::println)`.


## Stream filtering

Filtering streams of data is one of the most important abilities of streams. The  
`filter` method is an intermediate operation which returns a stream consisting  
of the elements of a stream that match the given predicate. A predicate is a  
method that returns a boolean value.    

```java
import java.util.Arrays;
import java.util.stream.IntStream;

void main() {

    IntStream nums = IntStream.rangeClosed(0, 25);

    int[] vals = nums.filter(e -> e > 15).toArray();

    System.out.println(Arrays.toString(vals));
}
```

The code example creates a stream of integers. The stream is filtered to contain  
only values greater than fifteen.  

```java
IntStream nums = IntStream.rangeClosed(0, 25);
```

With `IntStream`, a stream of twenty six integers is created. The `rangeClose`  
method creates a stream of integers from a bound of two values; these two values  
(start and end) are both included in the range.  

```java
int[] vals = nums.filter(e -> e > 15).toArray();
```

We pass a lambda expression `e -> e > 15` into the filter function; the  
expression returns true for values greater than 15. The `toArray` is a terminal  
operation that transforms a stream into an array of integers.  

```java
System.out.println(Arrays.toString(vals));
```

The array is printed to the console.  

```java
import java.util.stream.IntStream;

void main() {

    IntStream nums = IntStream.rangeClosed(0, 30);
    nums.filter(this::isEven).forEach(System.out::println);
}

boolean isEven(int e) {

    return e % 2 == 0;
}
```
 
To get even numbers from a stream, we pass an isEven method reference to the  
filter method.  

```java
nums.filter(this::isEven).forEach(System.out::println);
```

The double colon `::` operator is used to pass a method reference. The `forEach`  
method is a terminal operation that iterates over the elements of the stream. It  
takes a method reference to the `System.out.println` method.  

# Skipping and limiting elements

The `skip(n)` method skip the first `n` elements of the stream and the `limit(m)`  
method limits the number of elements in the stream to `m`.  

```java
import java.util.stream.IntStream;

void main() {

    IntStream s = IntStream.range(0, 15);
    s.skip(3).limit(5).forEach(System.out::println);
}
```

The example creates a stream of fifteen integers. We skip the first three  
elements with the skip method and limit the number of elements to ten values.  


## Sorting elements

The `sorted` method sorts the elements of this stream, according to the provided  
`Comparator`.  

```java
import java.util.Comparator;
import java.util.stream.IntStream;

void main() {

    IntStream nums = IntStream.of(4, 3, 2, 1, 8, 6, 7, 5);

    nums.boxed().sorted(Comparator.reverseOrder())
            .forEach(System.out::println);
}
```

The example sorts integer elements in a descending order. The `boxed` method  
converts `IntStream` to `Stream<Integer>`.  

The next example shows how to compare a stream of objects.  

```java
import java.util.Comparator;
import java.util.List;

record Car(String name, int price) {}

void main() {

    List<Car> cars = List.of(new Car("Citroen", 23000),
            new Car("Porsche", 65000), new Car("Skoda", 18000),
            new Car("Volkswagen", 33000), new Car("Volvo", 47000));

    cars.stream().sorted(Comparator.comparing(Car::price))
            .forEach(System.out::println);
}
```

The example sorts cars by their price.

```java
List<Car> cars = List.of(new Car("Citroen", 23000),
    new Car("Porsche", 65000), new Car("Skoda", 18000),
    new Car("Volkswagen", 33000), new Car("Volvo", 47000));
```

A list of cars is created.

```java
cars.stream().sorted(Comparator.comparing(Car::price))
    .forEach(System.out::println);
```

A stream is generated from a list using the stream method. We pass a reference  
to the Car's price method, which is used when comparing cars by their price.  


## Unique values

The `distinct` method returns a stream consisting of unique elements.

```java
import java.util.Arrays;
import java.util.stream.IntStream;

void main() {

    IntStream nums = IntStream.of(1, 1, 3, 4, 4, 6, 7, 7);
    int a[] = nums.distinct().toArray();

    System.out.println(Arrays.toString(a));
}
```

The example removes duplicate values from a stream of integers.  

```java
IntStream nums = IntStream.of(1, 1, 3, 4, 4, 6, 7, 7);
```

There are three duplicate values in the stream.

```java
int a[] = nums.distinct().toArray();
```

We remove the duplicates with the `distinct` method.  


# Mapping

It is possible to change elements into a new stream; the original source is not    
modified. The map method returns a stream consisting of the results of applying  
the given function to the elements of a stream. The map is an itermediate  
operation.  

```java
import java.util.Arrays;
import java.util.stream.IntStream;

void main() {

    IntStream nums = IntStream.of(1, 2, 3, 4, 5, 6, 7, 8);
    int[] squares = nums.map(e -> e * e).toArray();

    System.out.println(Arrays.toString(squares));
}
```

We map a transformation function on each element of the stream.  

```java
int[] squares = nums.map(e -> e * e).toArray();
```

We apply a lamda expression `e -> e * e` on the stream: each of the elements is  
squared. A new stream is created which is transformed into an array with the  
toArray method.  

In the next example, we transform a stream of strings.  

```java
import java.util.stream.Stream;

void main() {

    Stream<String> words = Stream.of("cardinal", "pen", "coin", "globe");
    words.map(this::capitalize).forEach(System.out::println);
}

String capitalize(String word) {

    word = word.substring(0, 1).toUpperCase() + word.substring(1).toLowerCase();
    return word;
}
```

We have a stream of strings. We capitalize each of the strings of the stream.  

```java
words.map(this::capitalize).forEach(System.out::println);
```

We pass a reference to the capitalize method to the `map` method.  

## Reductions

A reduction is a terminal operation that aggregates a stream into a type or a  
primitive.  

```java
import java.util.stream.IntStream;

void main() {

    IntStream nums = IntStream.of(1, 2, 3, 4, 5, 6, 7, 8);
    int maxValue = nums.max().getAsInt();

    System.out.printf("The maximum value is: %d%n", maxValue);
}
```

Getting a maximum value from a stream of integers is a reduction operations.  

```java
int maxValue = nums.max().getAsInt();
```

With the `max` method, we get the maximum element of the stream. The method  
returns an `Optional` from which we get the integer using the `getAsInt` method.

A custom reduction can be created with the `reduce` method.  

```java
import java.util.stream.IntStream;

void main() {

    IntStream nums = IntStream.of(1, 2, 3, 4, 5, 6, 7, 8);

    int product = nums.reduce((a, b) -> a * b).getAsInt();

    System.out.printf("The product is: %d%n", product);
}
```

The example returns a product of the integer elements in the stream.  


## Collection operations

A collection is a terminal reduction operation which reduces elements of a  
stream into a Java collection, string, value, or specific grouping.  

```java
import java.util.List;

record Car(String name, int price) {
}

void main() {

    List<Car> cars = List.of(new Car("Citroen", 23000),
            new Car("Porsche", 65000), new Car("Skoda", 18000),
            new Car("Volkswagen", 33000), new Car("Volvo", 47000));

    List<String> names = cars.stream().map(Car::name)
            .filter(name -> name.startsWith("Vo"))
            .toList();

    for (String name : names) {

        System.out.println(name);
    }
}
```

The example creates a stream from a list of car object, filters the cars by the  
their name, and returns a list of matching car names.  

```java
List<String> names = cars.stream().map(Car::name)
        .filter(name -> name.startsWith("Vo"))
        .toList();
```

At the end of the pipeline, we use the `collect` method to transform.  


In the next example, we use the `collect` method to group data.  

```java
import java.util.List;
import java.util.Map;
import java.util.function.Function;
import java.util.stream.Collectors;

void main() {

    List<String> items = List.of("pen", "book", "pen", "coin",
            "book", "desk", "book", "pen", "book", "coin");

    Map<String, Long> result = items.stream().collect(
            Collectors.groupingBy(
                    Function.identity(), Collectors.counting()
            ));

    for (Map.Entry<String, Long> entry : result.entrySet()) {

        String key = entry.getKey();
        Long value = entry.getValue();

        System.out.format("%s: %d%n", key, value);
    }
}
```

The code example groups elements by their occurrence in a stream.  

```java
Map<String, Long> result = items.stream().collect(
        Collectors.groupingBy(
                Function.identity(), Collectors.counting()
        ));
```

With the `Collectors.groupingBy` method, we count the occurrences of the  
elements in the stream. The operation returns a map.  

```java
for (Map.Entry<String, Long> entry : result.entrySet()) {

    String key = entry.getKey();
    Long value = entry.getValue();

    System.out.format("%s: %d%n", key, value);
}
```

We go through the map and print its key/value pairs.  
