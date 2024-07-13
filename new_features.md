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

## Primitive types in patterns 

```java
import java.util.Random;

void main() {

    boolean isGirl = new Random().nextBoolean();

    String name = pickName(isGirl);
    System.out.printf("chosen name: %s %n", name);
}

String pickName(boolean isGirl) {

    return switch (isGirl) {
        case true -> "Zuzana";
        case false -> "Martin";
    };
}
```

```java
import java.util.Arrays;

void main() {

    int[] ages = { 12, 23, 45, 0, 67, 88, 43, 55, -4};

    Arrays.stream(ages).forEach(e -> System.out.println(e + ": " + checkAge(e)));
}

String checkAge(int age) {

    return switch (age) {
        case int i when i < 18 && i > 0-> "minor";
        case int i when i >= 18 && i < 64 -> "adult";
        case int i when i > 64 -> "senior";
        default -> "n/a";
    };
}
```

