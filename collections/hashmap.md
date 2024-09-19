# HashMap
 
`HashMap` is a container that stores key-value pairs. Each key is associated  
with one value. Keys in a `HashMap` must be unique. `HashMap` is called an  
associative array or a dictionary in other programming languages. `HashMaps`  
take more memory because for each value there is also a key. Deletion and  
insertion operations take constant time. `HashMaps` can store `null` values.  

`HashMaps` do not maintain order.  
 
`Map.Entry` represents a key-value pair in `HashMap`. `HashMap's` `entrySet`  
returns a `Set` view of the mappings contained in the map. A set of keys is  
retrieved with the `keySet` method.

`HashMap` extends `AbstractMap` and implements `Map`. The `Map` provides method  
signatures including `get`, `put`, `size`, or `isEmpty`.  



## HashMap initialization

Creating an empty `HashMap` and initializing with `put` method. 

```java
import java.util.HashMap;
import java.util.Map;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    System.out.println(capitals);
}
```

## The Map.of method

The `Map.of` method returns an unmodifiable map.

```java
import java.util.Map;

void main() {

    Map<Integer, String> colours = Map.of(1, "red", 2, "blue", 3, "brown");
    System.out.println(colours);
}
```


## The Map.ofEntries method

The `Map.ofEntries` returns an unmodifiable map containing keys and values extracted  
from the given entries.  

```java
import java.util.Map;
import static java.util.Map.entry;

void main() {

    Map<String, String> countries = Map.ofEntries(
            entry("de", "Germany"),
            entry("sk", "Slovakia"),
            entry("ru", "Russia"));

    System.out.println(countries);
}
```


Older syntax:  

```java
import java.util.HashMap;
import java.util.Map;

// up to Java 8
void main() {

    Map countries = new HashMap<>() {
        {
            put("de", "Germany");
            put("sk", "Slovakia");
            put("ru", "Russia");
        }
    };

    System.out.println(countries);
}
```

In this example we create a modifiable hashmap. This way of initialization is  
dubbed double-braced hashmap initialization.  

## Modifiable HashMap

We create a modifiable hashmap. 

```java
import java.util.HashMap;
import java.util.Map;


void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    System.out.println(capitals);

    capitals.putIfAbsent("rus", "Moscow");
    capitals.putIfAbsent("ita", "Rome");

    System.out.println(capitals);
}
```

First, we create a new `HashMap` object. Then we add elements with `put`.

```java
capitals.putIfAbsent("rus", "Moscow");
capitals.putIfAbsent("ita", "Rome");
```

We put new elements only if they are not already present with `putIfAbsent`. 

## The size method

The size of the `HashMap` is determined with the `size` method.

```java
import java.util.HashMap;
import java.util.Map;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    int size = capitals.size();

    System.out.printf("The size of the HashMap is %d%n", size);

    capitals.remove("pol");
    capitals.remove("ita");

    size = capitals.size();

    System.out.printf("The size of the HashMap is %d%n", size);
}
```

In the code example, we create a `HashMap` and determine its size with size.  
Then we remove some pairs and determine its size again. We print the findings to  
the console.  

```java
capitals.put("svk", "Bratislava");
capitals.put("ger", "Berlin");
```

With put, we add new pairs into the HashMap.

```java
int size = capitals.size();
```

Here we get the size of the map.

```java
capitals.remove("pol");
capitals.remove("ita");
```

With remove, we delete two pairs from the map.

## The get method

To retrieve a value from a `HashMap`, we use the get method. It takes a key as a  
parameter.  

```java
import java.util.HashMap;
import java.util.Map;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    String cap1 = capitals.get("ita");
    String cap2 = capitals.get("svk");

    System.out.println(cap1);
    System.out.println(cap2);
}
```

In the example, we retrieve two values from the map.

```java
String cap2 = capitals.get("svk");
```

Here we get a value which has "svk" key.

## The clear method

The `clear` method removes all pairs from the `HashMap`.

```java
import java.util.HashMap;
import java.util.Map;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    capitals.clear();

    if (capitals.isEmpty()) {

        System.out.println("The map is empty");
    } else {

        System.out.println("The map is not empty");
    }
}
```

In the example, we remove all elements and print the size of the map to the  
console.  

```java
capitals.clear();
```

We remove all pairs with clear.

```java
if (capitals.isEmpty()) {

    System.out.println("The map is empty");
} else {

    System.out.println("The map is not empty");
}
```

With the `isEmpty` method, we check if the map is empty.  

## The containsKey method

The `containsKey` method returns `true` if the map contains a mapping for the
specified key.  

```java
import java.util.HashMap;
import java.util.Map;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    String key1 = "ger";
    String key2 = "rus";

    if (capitals.containsKey(key1)) {

        System.out.printf("HashMap contains %s key%n", key1);
    } else {

        System.out.printf("HashMap does not contain %s key%n", key1);
    }

    if (capitals.containsKey(key2)) {

        System.out.printf("HashMap contains %s key%n", key2);
    } else {

        System.out.printf("HashMap does not contain %s key%n", key2);
    }
}
```

In the example, we check if the map contains two keys.

```java
if (capitals.containsKey(key1)) {

    System.out.printf("HashMap contains %s key%n", key1);
} else {

    System.out.printf("HashMap does not contain %s key%n", key1);
}
```

This if statement prints a message depending on whether the map contains the  
given key.  

## Practical usage

The following program calcuates the frequency of characters in the string.  

```java
import java.util.HashMap;
import java.util.Map;

void main() {

    String message = "there is an old falcon in the sky";

    Map<Character, Integer> charFreq = new HashMap<>();

    for (Character c : message.toCharArray()) {

        // Check if the character already exists in the map
        if (charFreq.containsKey(c)) {
            // Increment the frequency count for the existing character
            charFreq.put(c, charFreq.get(c) + 1);
        } else {
            // Add the character to the map with a frequency of 1
            charFreq.put(c, 1);
        }
    }

    System.out.println(charFreq);
}
```


## The replace method

There are `replace` methods which enable programmers to replace entries.

```java
replace(K key, V value)
```

This method replaces the entry for the specified key only if it is currently  
mapped to some value.  

```java
replace(K key, V oldValue, V newValue)
```

This method replaces the entry for the specified key only if it is currently  
mapped to the specified value.  

```java
import java.util.HashMap;
import java.util.Map;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("day", "Monday");
    capitals.put("country", "Poland");
    capitals.put("colour", "blue");

    capitals.replace("day", "Sunday");
    capitals.replace("country", "Russia", "Great Britain");
    capitals.replace("colour", "blue", "green");

    capitals.entrySet().forEach(System.out::println);
}
```

In the example, we replace pairs in the map with replace.

```java
capitals.replace("day", "Sunday");
```

Here we replace a value for the "day" key.

```java
capitals.replace("country", "Russia", "Great Britain");
```

In this case, the value is not replaced because the key is not currently set to  
"Russia".  

```java
capitals.replace("colour", "blue", "green");
```

Because the old value is correct, the value is replaced.

## Convert HashMap to List

In the next example we convert HashMap entries to a list of entries.  

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Map;
import java.util.Set;

void main() {

    Map<String, String> colours = Map.of(
            "AliceBlue", "#f0f8ff",
            "GreenYellow", "#adff2f",
            "IndianRed", "#cd5c5c",
            "khaki", "#f0e68c"
    );

    Set<Map.Entry<String, String>> entries = colours.entrySet();
    List<Map.Entry<String, String>> mylist = new ArrayList<>(entries);

    System.out.println(mylist);
}
```

The `entrySet` returns a set view of mappings, which is later passed to the  
constructor of the `ArrayList`.  

## Iteration with forEach

We use the `forEach` method to iterate over the key-value pairs of the  
`HashMap`. The `forEach` method performs the given action for each element of  
the map until all elements have been processed or the action throws an  
exception.

```java
import java.util.HashMap;
import java.util.Map;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    capitals.forEach((k, v) -> System.out.format("%s: %s%n", k, v));
}
```

In the code example, we iterate over a `HashMap` with `forEach` using a lambda  
expression.  

```java
capitals.forEach((k, v) -> System.out.format("%s: %s%n", k, v));
```

With `forEach` we iterate over all pairs of the map.

## Iteration with enhanced for loop

The enhanced for loop can be used to iterate over a `HashMap`.

```java
import java.util.HashMap;
import java.util.Map;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    for (Map.Entry<String, String> pair: capitals.entrySet()) {

        System.out.format("%s: %s%n", pair.getKey(), pair.getValue());
    }
}
```

In the example we iterate over a `HashMap` with enhanced for loop.

```
for (Map.Entry<String, String> pair: capitals.entrySet()) {

    System.out.format("%s: %s%n", pair.getKey(), pair.getValue());
}
```

In each for cycle, a new key-value couple is assigned to the pair variable.  

With type inference, we can shorten the code a bit.  

```java
import java.util.HashMap;
import java.util.Map;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    for (var pair: capitals.entrySet()) {

        System.out.format("%s: %s%n", pair.getKey(), pair.getValue());
    }
}
```

We shorten the code by using a var keyword in the for loop.  

## Iteration over keys

We might want to iterate only over keys of a `HashMap`.  

```java
import java.util.HashMap;
import java.util.Map;
import java.util.Set;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    Set<String> keys = capitals.keySet();

    keys.forEach(System.out::println);
}
```

The example iterates over keys of the capitals map.

```java
Set keys = capitals.keySet();
```

The keys of a `HashMap` are retrieved with the `keySet` method, which returns a  
`Set` of keys. Keys must be unique; therefore, we have a `Set`. `Set` is a  
collection that contains no duplicate elements.  

```java
keys.forEach(System.out::println);
```

We go over the set of keys with `forEach`.  

## Iteration over values

We might want to iterate only over values of a `HashMap`.  

```java
import java.util.Collection;
import java.util.HashMap;
import java.util.Map;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    Collection<String> vals = capitals.values();

    vals.forEach(System.out::println);
}
```

The example iterates over values of a `HashMap`.

```java
Collection vals = capitals.values();
```

The values of a `HashMap` are retrieved with the `values` method.

```java
vals.forEach(System.out::println);
```

We go over the collection with `forEach`.

## Filtering HashMap

`HashMap` can be filtered with the `filter` method of the Java Stream API.  

```java
import java.util.HashMap;
import java.util.Map;
import java.util.stream.Collectors;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    Map<String, String> filteredCapitals = capitals.entrySet().stream()
            .filter(e -> e.getValue().length() == 6)
            .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));

    filteredCapitals.entrySet().forEach(System.out::println);
}
```

In the example, we filter the map to contain only pairs whose values' size is  
equal to six.  


## List of maps

In the next example, we have a list of maps.  

```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

void main() {

    Map<String,Integer> fruits1 = new HashMap<>();
    fruits1.put("oranges", 2);
    fruits1.put("bananas", 3);

    Map<String,Integer> fruits2 = new HashMap<>();
    fruits2.put("plums", 6);
    fruits2.put("apples", 7);

    List<Map<String,Integer>> all = new ArrayList<>();
    all.add(fruits1);
    all.add(fruits2);

    all.forEach(e -> e.forEach((k, v) -> System.out.printf("k: %s v %d%n", k, v)));
}
```

We define two maps and insert them into a list. Then we interate over the list
with two `forEach` loops.  

## Word occurences

### Using for loops 

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

void main() throws IOException {

    Map<String, Integer> wordCount = new HashMap<>();

    Path path = Paths.get("src/resources/thermopylae.txt");
    List<String> lines = Files.readAllLines(path);

    for (String line : lines) {

        String[] words = line.split("\\s+");

        for (String word : words) {

            if (!word.isEmpty()) {
                word = word.toLowerCase();
                wordCount.put(word, wordCount.getOrDefault(word, 0) + 1);
            }
        }
    }

    wordCount.forEach((k, v) -> System.out.printf("%s %d%n", k, v));
}
```


### Using streams

```java
import java.io.IOException;

import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.Arrays;
import java.util.Map;
import java.util.function.Function;
import java.util.stream.Collectors;
import java.util.stream.Stream;

void main(String[] args) throws IOException {

    Path filePath = Paths.get("src/resources/thermopylae.txt");

    try (Stream<String> lines = Files.lines(filePath)) {

        Map<String, Long> wordOccurrences = lines
                .flatMap(line -> Arrays.stream(line.trim().split("\\s+")))
                .map(word -> word.replaceAll("[^a-zA-Z]", "").toLowerCase().trim())
                .filter(word -> !word.isEmpty())
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));

        wordOccurrences.forEach((word, count) -> System.out.println(word + ": " + count));
    }
}
```

1. `Files.lines(Paths.get("file.txt"))`: Creates a `Stream<String>` where  
   each element is a line read from the file "file.txt".  
2. `.flatMap(line -> Arrays.stream(line.split("\\s+")))`: Splits each line  
   into words, and flattens all streams of words into one stream.  
3. `.filter(word -> word.length() > 0)`: Filters out any empty strings  
   that may have been created by the split operation.  
4. `.map(String::toLowerCase)`: Converts all words in the stream to lower  
   case.  
5. `.collect(Collectors.toList())`: Collects all elements of the stream  
   into a `List<String>`.  

The `flatMap` operation:  

In the provided code, `flatMap` is used to transform the `Stream<String>` of  
lines from the file into a `Stream<String>` of words. It takes each line, splits  
it into an array of words (using `split("\\s+")`), and then creates a stream  
from this array.   

The `flatMap` method then flattens all the individual streams of words into a  
single stream. This is necessary because after splitting, you have a stream of  
arrays, and you want to have a stream of words instead. The flatMap operation  
flattens the structure from `Stream<String[]>` to `Stream<String>`, allowing  
further operations like filtering and collecting to work on individual words  
rather than arrays of words.  
