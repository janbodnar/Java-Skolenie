# New features 

## Unnamed variables & patterns 

```java
import java.util.List;

sealed interface Item permits Book, Rock, Tool {}

record Book() implements Item {}
record Rock() implements Item {}
record Tool() implements Item {}

void main() {

    for (int _ : new int[]{1, 2, 3, 4, 5}) {
        System.out.println("falcon");
    }

    var items = List.of(new Book(), new Rock(), new Rock(), new Tool());

    for (var item : items) {

        switch (item) {
            case Book _ -> System.out.println("it is a book");
            case Rock _ -> System.out.println("it is a rock");
            case Tool _ -> System.out.println("it is a tool");
            default -> System.out.println("unknown");
        }
    }
}
```
