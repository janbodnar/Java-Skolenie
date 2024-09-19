# Priklady

## Calculate sum

```java
void main() {

    int sum = 0;
    int[] vals = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

    for (int i = 0; i< vals.length; i++) {

        sum = sum + vals[i];
    }

    System.out.println(sum);
}
```

```java
void main() {

    int[] vals = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int sum = 0;

    for (int val: vals) {
        sum = sum + val;
    }

    System.out.println(sum);

    System.out.println("end of program");
}
```


## Formatovany vystup

```java
void main() {

    int age = 34;
    String name = "William";
    String occupation = "gardener";
    float weight = 78.5f;

    String output = String.format("%s is %d years old and he is a %s, his weight is %f kg", name, age, occupation, weight);
    System.out.println(output);
    
    System.out.printf("%s is %d years old and he is a %s, his weight is %f kg", name, age, occupation, weight);
}
```

## Premenne

```java
void main() {

    String name = "John Doe";
    int age = 34;

    System.out.println(name);
    System.out.println(age);

    name = "Roger Roe";
    System.out.println(name);

    age = 40;
    System.out.println(age);
}
```


```java
void main() {

    String name = "John Doe";
    int age = 34;
    String occupation = "gardener";

    System.out.println(name + " is " + age + " years old" + " and he is a " + occupation );
}
```
