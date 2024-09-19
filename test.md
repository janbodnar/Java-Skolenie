# Priklady


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
