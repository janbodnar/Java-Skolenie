# Samples

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
