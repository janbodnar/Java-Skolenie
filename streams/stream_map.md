# Mapping

The map method returns a stream consisting of the results of applying the given  
function to the elements of a stream. The map is an itermediate operation.  

We change stream elements into a new stream; the original source is not  
modified.  

## Example I

In the first example, we map an arithmetic operation on a list of values.  

```java
import java.util.Arrays;
import java.util.stream.IntStream;

void main() {

    var nums = IntStream.of(1, 2, 3, 4, 5, 6, 7, 8);
    var squares = nums.map(e -> e * e).toArray();

    System.out.println(Arrays.toString(squares));
}
```

In the example, we create a stream of integers. With the map method we apply an  
arithmetic operation on the values and then transform them into an array.  


## Example II

In the following example, we use map and mapToInt methods in one stream.  

```java
import java.util.Random;
import java.util.stream.Stream;

void main() {

    Stream.generate(new Random()::nextDouble)
            .map(e -> (e * 100))
            .mapToInt(Double::intValue)
            .limit(5)
            .forEach(System.out::println);
}
```

The example generates five random double values. Using the mapping methods, each  
of the randomly generated values is multiplied by 100 and transformed into   
integer.  


## Example III

In the next example, we map a custom method on a stream of strings.  

```java
import java.util.stream.Stream;

void main() {

    var words = Stream.of("cardinal", "pen", "coin", "globe");
    words.map(this::capitalize).forEach(System.out::println);
}

String capitalize(String word) {

    word = word.substring(0, 1).toUpperCase() + word.substring(1).toLowerCase();
    return word;
}
```

The example capitalizes each of the words in the stream.


## Example IV

In the next example, we read values from a CSV file into a list using map  
methods.   

```
2,3,5,6,1,0
9,5,6,3,2,1
```

We have these values in the `numbers.csv` file.

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.Arrays;
import java.util.Collection;
import java.util.stream.Collectors;

void main() throws IOException {

    var lines = Files.readAllLines(Path.of("src/resources/numbers.csv"));

    var vals = lines.stream().map(line-> Arrays.asList(line.split(",")))
            .flatMap(Collection::stream).mapToInt(Integer::valueOf)
            .boxed().collect(Collectors.toList());

    System.out.println(vals);
}
```

First, we read the CSV file into a list of strings. Then we create a stream from  
the list and apply mapping methods to get a list of integers in the end.  

The `flatMap` is used to convert a stream of lists into a stream of elements.  

1. `lines.stream()` creates a stream from the list of lines read from the file.  
2. `.map(line -> Arrays.asList(line.split(",")))` transforms each line into a  
   list of strings, splitting each line by commas.  
3. `.flatMap(Collection::stream)` takes each list created by the map operation  
   and 'flattens' it into individual elements, creating a single stream of  
   strings.  
4. `.mapToInt(Integer::valueOf)` converts each string in the stream to an integer.  
5. `.boxed()` converts the `IntStream` back to a `Stream<Integer>`.  
6. `.collect(Collectors.toList())` collects the elements of the stream into a list.  

The `flatMap` flattens the lists of strings into a single stream before they are  
converted to integers and collected into a list.  


## Example V

In the next example, we use map operations on a list of user objects.

```java
import java.util.Comparator;
import java.util.List;
import java.util.stream.Collectors;

void main() {

    var users = List.of(new User("Peter", "programmer"),
            new User("Jane", "accountant"), new User("Robert", "teacher"),
            new User("Milan", "programmer"), new User("Jane", "designer"));

    var userNames = users.stream().map(User::name).sorted()
            .collect(Collectors.toList());
    System.out.println(userNames);

    var occupations = users.stream().map(User::occupation)
            .sorted(Comparator.reverseOrder()).distinct()
            .collect(Collectors.toList());

    System.out.println(occupations);
}

record User(String name, String occupation) {

}
```

The example creates a list of sorted names from a list of users and a list of  
unique occupations in a reverse order.  

