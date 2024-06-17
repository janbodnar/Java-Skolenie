# Filtering ArrayList 


## A list of words

Using for loop.  

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    var words = List.of("sky", "tent", "war", "water", "warm",
            "cup", "cloud", "pen", "forest", "atom", "peril", "wood", "falcon");

    var filtered = new ArrayList<String>();

    for (var word : words) {
        if (word.startsWith("w")) {
            filtered.add(word);
        }
    }
    filtered.forEach(System.out::println);
}
```

Using streams.  

```java
import java.util.List;

void main() {

    var words = List.of("sky", "tent", "war", "water", "warm",
            "cup", "cloud", "pen", "forest", "atom", "peril", "wood", "falcon");

    var res = words.stream().filter(word -> word.startsWith("w")).toList();
    res.forEach(System.out::println);
}
``

