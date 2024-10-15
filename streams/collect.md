# Collecting

The `collect` is a terminal stream operation. It performs a mutable reduction  
operation on the elements of the stream. Reduction operations can be performed  
either sequentially or in parallel.  

## Collectors

The `Collectors` class contains predefined collectors to perform common mutable  
reduction tasks. The collectors accumulate elements into collections, reduce  
elements into a single value (such as min, max, count, or sum), or group  
elements by a criteria.  

```java
Set<String> uniqueVals = vals.collect(Collectors.toSet());
```

The `toSet` method returns a `Collector` that accumulates the input elements  
into a new `Set`.  

```java
// can be replaced with min()
Optional<Integer> min = vals.stream().collect(Collectors.minBy(Integer::compareTo));
```

The minBy returns a `Collector` that produces the minimal element according to a  
given `Comparator`.  

```java
Map<Boolean, List<User>> usersByStatus =
    users().stream().collect(Collectors.groupingBy(User::isSingle));
```

With `groupingBy` we select users who have single status into a group.

```java
Map<Boolean, List<User>> statuses =
    users().stream().collect(Collectors.partitioningBy(User::isSingle));
```

With `partitioningBy` we separate the users into two groups based on their  
status attribute.  

## Collector

The `Collector` interface defines a set of methods which are used during the  
reduction process. The following is the interface signature with the five  
methods it declares.  

```java
public interface Collector<T,A,R> {
    Supplier<A> supplier();
    BiConsumer<A,T> accumulator();
    BinaryOperator<A> combiner();
    Function<A,R> finisher();
    Set<Characteristics> characteristics();
}
```

A `Collector` is specified by four functions that work together to accumulate  
entries into a mutable result container, and optionally perform a final  
transform on the result.  

The `T` is the type of elements in the stream to be collected. The `A` the type  
of the accumulator. The `R` is the type of the result returned by the collector.  

The supplier returns a function which creates a new result container. The  
accumulator returns a function which performs the reduction operation. It  
accepts two arguments: the first ist the mutable result container (accumulator)  
and the second the stream element that is folded into the result container.  

When the stream is collected in parallel the combiner returns a function which  
merges two accumulators. The finisher returns a function which performs the  
final transformation from the intermediate result container to the final result  
of type `R`. The finisher returns an identity function when the accumulator  
already represents the final result.  

Note: In math, the identity function is one in which the output of the function  
is equal to its input. In Java, the identity method of a `Function` returns a  
`Function` that always returns its input arguments. The characteristics method  
returns an immutable set of Characteristics which define the behavior of the  
collector. It can be used to do some optimizations during the reduction process.  
For example, if the set contains CONCURRENT, then the collection process can be  
performed in parallel.  

## Collectors.toList

The `Collectors.toList` returns a collector that accumulates the input elements  
into a new list.  

```java
import java.util.List;
import java.util.stream.Collectors;

void main() {

    var words = List.of("marble", "coin", "forest", "falcon",
            "sky", "cloud", "eagle", "lion");

    // filter all four character words into a list
    var words4 = words.stream().filter(word -> word.length() == 4)
            .collect(Collectors.toList());

    System.out.println(words4);
}
```

The example filters a list of strings and transforms the stream into a list. We  
filter the list to include only strings whose length is equal to four.  

```java
var words4 = words.stream().filter(word -> word.length() == 4)
    .collect(Collectors.toList());
```

With the stream method, we create a Java Stream from a list of strings. On this  
stream, we apply the filter method. The filter method accepts an anonymous  
function that returns a boolean true for all elements of the stream whose length  
is four. We create a list back from the stream with the collect method.  

## Collectors.joining

The `Collectors.joining` returns a `Collector` that concatenates the input  
elements into a string, in encounter order.  

```java
import java.util.List;
import java.util.stream.Collectors;

void main(String[] args) {

    var words = List.of("marble", "coin", "forest", "falcon",
            "sky", "cloud", "eagle", "lion");

    // can be replaced with String.join
    var joined = words.stream().collect(Collectors.joining(","));

    System.out.printf("Joined string: %s", joined);
}
```

We have a list of words. We transform the list into a string where the words are  
separated with comma.  


## Collectors.counting

The `Collectors.counting` retuns a Collector that counts the number of elements  
in the stream.  

```java
import java.util.List;
import java.util.stream.Collectors;

void main(String[] args) {

    var vals = List.of(1, 2, 3, 4, 5);

    // can be replaced with count
    var n = vals.stream().collect(Collectors.counting());

    System.out.println(n);
}
```

The example counts the number of elements in the list.


## Collectors.summingInt

The `Collectors.summingInt` returns a `Collector` that produces the sum of a  
integer-valued function applied to the input elements.  

```java
import java.util.List;
import java.util.stream.Collectors;

void main() {

    var cats = List.of(
            new Cat("Bella", 4),
            new Cat("Othello", 2),
            new Cat("Coco", 6)
    );

    // can be replaced with mapToInt().sum()
    var ageSum = cats.stream().collect(Collectors.summingInt(cat -> cat.age()));

    System.out.printf("Sum of cat ages: %d%n", ageSum);
}

record Cat(String name, int age) {}
```

The example sums the age of the cats.

```java
var ageSum = cats.stream().collect(Collectors.summingInt(cat -> cat.age()));
```

The parameter of the `summingInt` method is a mapper function which extracts the  
property to be summed.  

## Collectors.collectingAndThen

The `Collectors.collectingAndThen` adapts a `Collector` to perform an additional  
finishing transformation.  

```java
import java.text.NumberFormat;
import java.util.List;
import java.util.Locale;
import java.util.stream.Collectors;


void main() {

    var vals = List.of(230, 210, 120, 250, 300);

    var avgPrice = vals.stream().collect(Collectors.collectingAndThen(
            Collectors.averagingInt(Integer::intValue),
            avg -> {
                var nf = NumberFormat.getCurrencyInstance(Locale.US);
                return nf.format(avg);
            })
    );

    System.out.printf("The average price is %s%n", avgPrice);
}
```

The example calculates an average price and then formats it.


## Custom collector with Collector.of

The `Collector.of` returns a new `Collector` described by the given supplier,  
accumulator, combiner, and finisher functions.  

In the following example, we create a custom collector.  

```java
import java.util.List;
import java.util.StringJoiner;
import java.util.stream.Collector;

void main() {

    List<User> persons = List.of(
            new User("Robert", 28),
            new User("Peter", 37),
            new User("Lucy", 23),
            new User("David", 28));

    Collector<User, StringJoiner, String> personNameCollector =
            Collector.of(
                    () -> new StringJoiner(" | "), // supplier
                    (j, p) -> j.add(p.name()),  // accumulator
                    (j1, j2) -> j1.merge(j2),      // combiner
                    StringJoiner::toString);       // finisher

    String names = persons
            .stream()
            .collect(personNameCollector);

    System.out.println(names);
}

record User(String name, int age) {}
```

In the example, we collect the names from the list of user objects.  

```java
Collector<User, StringJoiner, String> personNameCollector =
...
```

The `Collector<User, StringJoiner, String>` has three types. The first is the  
type of input elements for the new collector. The second is the type for the  
intermediate result and the third for the final result.  

```java
Collector.of(
        () -> new StringJoiner(" | "), // supplier
        (j, p) -> j.add(p.getName()),  // accumulator
        (j1, j2) -> j1.merge(j2),      // combiner
        StringJoiner::toString);       // finisher
```

We create our custom collector. First, we build an initial result container. In  
our case it is a `StringJoiner`. The accumulator simply adds the name from the  
current user object to the `StringJoiner`. The combiner merges two partial  
results in case of parallel processing. Finally, the finisher turns the  
`StringJoiner` into a plain string.


## Collectors.groupingBy

With the `Collectors.groupingBy` method we can separate the stream elements into  
groups based on the specified criterion.  

```java
import java.math.BigDecimal;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

void main() {

    Map<String, List<Product>> productsByCategories =
            products().stream().collect(
                    Collectors.groupingBy(Product::category));

    productsByCategories.forEach((k, v) -> {

        System.out.println(k);

        for (var name : v) {
            System.out.println(name);
        }
    });

}

List<Product> products() {

    return List.of(
        new Product("apple", "fruit", new BigDecimal("4.50")),
        new Product("banana", "fruit", new BigDecimal("3.76")),
        new Product("carrot", "vegetables", new BigDecimal("2.98")),
        new Product("potato", "vegetables", new BigDecimal("0.92")),
        new Product("garlic", "vegetables", new BigDecimal("1.32")),
        new Product("ginger", "vegetables", new BigDecimal("2.45")),
        new Product("white bread", "bakery", new BigDecimal("1.50")),
        new Product("roll", "bakery", new BigDecimal("0.08")),
        new Product("bagel", "bakery", new BigDecimal("0.15"))
    );
}

record Product(String name, String category, BigDecimal price) {}
```

We have a list of products. With the `Collectors.groupingBy`, we separate the  
products into groups based on their category.  


## Collectors.partitioningBy

Partitioning is a special case of grouping. Partitioning operation divides the  
stream into two groups based on the given predicate function.  

We will group user objects.  

```java
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

void main() {

    Map<Boolean, List<User>> statuses =
            users().stream().collect(
                    Collectors.partitioningBy(User::single));

    statuses.forEach((k, v) -> {

        if (k) {

            System.out.println("Single: ");
        } else {

            System.out.println("In a relationship:");
        }

        v.forEach(System.out::println);
    });
}

List<User> users() {

    return List.of(
            new User("Julia", false),
            new User("Jake", false),
            new User("Mike", false),
            new User("Robert", true),
            new User("Maria", false),
            new User("Peter", true)
    );
}

record User(String name, boolean single) {
}
```

In the example, we partition the stream into two groups based on the single  
attribute.  

```java
Map<Boolean, List<User>> statuses =
    users().stream().collect(Collectors.partitioningBy(User::isSingle));
```

The `Collectors.partitioningBy` takes the `isSingle` predicate, which returns a  
boolean value indicating the status of the user.  

