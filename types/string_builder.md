# StringBuilder 

Java `String` objects are immutable; it is only possible to create mofied copies  
of the original string. When we need to modify strings in-place, we use  
`StringBuilder`.

`StringBuilder` is a mutable sequence of characters. `StringBuilder` is used  
when we want to modify Java strings in-place. `StringBuffer` is a thread-safe  
equivalent similar of `StringBuilder`.  

`StringBuilder` has methods such as `append`, `insert`, or `replace` that allow  
to modify strings.  

# Constructors


## StringBuilder is mutable

Java `String` is immutable while `StringBuilder` is mutable.

```java
void main() {
    
    var word = "rock";
    var word2 = word.replace('r', 'd');

    System.out.println(word2);

    var builder = new StringBuilder("rock");
    builder.replace(0, 1, "d");

    System.out.println(builder);
}
```

The example demonstrates the main difference between `String` and `StringBuilder`.

## The append method

`StringBuilder` contains several overload append methods that add a value at the  
end of the string.  

```java
import java.util.stream.LongStream;

final long MAX_VAL = 500;

void main() {

    var builder = new StringBuilder();
    var sum = LongStream.rangeClosed(0, MAX_VAL).sum();
    
    LongStream.rangeClosed(1, MAX_VAL).forEach(e -> {
    
        builder.append(e);
        
        if (e % 10 == 0) {
            builder.append("\n");
        }
        
        if (e < MAX_VAL) {
            builder.append(" + ");
        } else {
            builder.append(" = ");
        }
    });
    
    builder.append(sum);
    
    System.out.println(builder);
}
```

The example builds one big string from hundreds of small strings. The string has  
the following form: `1 + 2 + 3 + ... + MAX_VAL = SUM`.  


## The insert method

The `insert` method is used to insert a string into the specified position of  
the builder.  


```java
void main() {
    
    var sentence = "There is a red fox in the forest.";
    var builder = new StringBuilder(sentence);

    builder.insert(19, "and a wolf ");

    System.out.println(builder);
}
```


## Getting indexes of substrings

The `indexOf` method returns the first occurrence of a substring while the  
`lastIndexOf` method returns the last occurrence.  

```java
void main() {
        
    var builder = new StringBuilder();
    
    builder.append("There is a wolf in the forest. ");
    builder.append("The wolf appeared very old. ");
    builder.append("I never saw a wild wolf in my life.");

    var term = "wolf";

    int firstIdx = builder.indexOf(term);
    int firstIdx2 = builder.indexOf(term, 15);

    System.out.format("First occurrence of %s %d%n", term, firstIdx);
    System.out.format("First occurrence of %s %d%n", term, firstIdx2);

    int lastIdx = builder.lastIndexOf(term);
    int lastIdx2 = builder.lastIndexOf(term, 15);

    System.out.format("Last occurrence of %s %d%n", term, lastIdx);
    System.out.format("Last occurrence of %s %d%n", term, lastIdx2);

    System.out.println(builder);
}
```

The example uses the `indexOf` and `lastIndexOf` methods to get the indexes of  
the "wolf" substring.


## The replace method

The `replace` method replaces a substring in the string builder with the  
specified new string.  

```java
void main() {
    
    var sentence = "I saw a red fox running into the forest.";
    var builder = new StringBuilder(sentence);

    var term = "fox";
    var newterm = "dog";

    int idx = builder.indexOf(term);
    int len = term.length();

    builder.replace(idx, idx + len, newterm);

    System.out.println(builder);
}
```


## Deleting characters

There are two methods for deleting characters in a string builder.  

```java
void main() {
    
    var sentence = "There is a red fox in the forest.";
    var builder = new StringBuilder(sentence);

    builder.delete(11, 14);
    System.out.println(builder);

    builder.deleteCharAt(11);
    System.out.println(builder);
}
```

The example deletes a few characters from a string.  


## Substrings

With the substring method it is possible to return substrings from a string.  

```java
void main() {
    
    var sentence = "There is a red fox in the forest.";
    var builder = new StringBuilder(sentence);

    var word = builder.substring(15, 18);
    System.out.println(word);

    var sbstr = builder.substring(15);
    System.out.println(sbstr);
}
```


