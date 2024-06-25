# Samples


## enum

```java
enum Season {
    SPRING,
    SUMMER,
    AUTUMN,
    WINTER
}


void main() {

    Season s1 = Season.AUTUMN;
    System.out.println(s1);

    Season s2 = Season.WINTER;
    System.out.println(s2);

    for (Season season : Season.values()) {
        System.out.println(season);
    }
}
```


## and/or operators 

```java
void main() {

    String[] words = {"sky", "war", "atom", "water", "warm", "cup", "cloud"};

    for (String word : words) {

        if (word.startsWith("w") && (word.length() == 3 || word.length() == 4)) {

            System.out.println(word);
        }
    }
}
```

---

```java
void main() {

    int[] vals = {1, -2, 0, 1, -1, 5, 10, -6};

    for (int val : vals) {

        if (val % 2 == 0 && val < 0) {
            System.out.println(val);
        }
    }
}
```


## and operator

```java
void main() {


    String[] words = {"sky", "war", "atom", "water", "warm", "cup", "cloud"};

    for (String word : words) {

        if (word.startsWith("w") || word.startsWith("c") ) {

            System.out.println(word);
        }

    }
}
```


## Sum for loop

```java
void main() {

    int[] vals = {10, 25, 30, 45, 50};
    int sum = 0;

    for (int i = 0; i < vals.length; i++) {

        sum = sum + vals[i];
    }

    System.out.println(sum);
}
```

## Even/odd sum

```java
void main() {

    int[] vals = {10, 25, 30, 45, 50};
    int sum = 0;

    for (int val : vals) {
        if (val % 2 == 1) {
            sum = sum + val;

        }
    }

    System.out.println(sum);
}
```

## Recap

```java
void main() {

    String name = "John Doe";
    int age = 34;
    String occupation = "gardener";

    System.out.printf("%s is %d years old and he is a %s%n", name, age, occupation);
    System.out.println(name + " is " + age + " years old and he is a " + occupation);

    String message = String.format("%s is %d years old and he is a %s%n", name, age, occupation);
    System.out.println(message);
}
```
