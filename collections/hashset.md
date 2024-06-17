# HashSet

`HashSet` is a collection that contains no duplicate elements. This class offers  
constant time performance for the basic operations (`add`, `remove`, `contains`,  
and `size`). `HashSet` does not provide ordering of elements. `HashSet` does not  
have a get method to retrieve elements.  

`HashSet` implements the `Set` interface. The `Set` is a collection with no  
duplicates. This interface models the mathematical set abstraction.  

## Initialization 

In Java, it's considered good practice to use the interface (`Set`) on the left  
side of an assignment and the implementation (`HashSet`) on the right side. This  
is known as "programming to an interface". It makes your code more flexible and  
easier to change because you can switch to a different `Set` implementation  
without changing the rest of your code.  

Here's a quick example:

```java
Set<String> brands = new HashSet<>();
```

If you later decide to use a `TreeSet` or a `LinkedHashSet` for performance  
reasons or order requirements, you only need to change the right side of the  
assignment:

```java
Set<String> brands = new TreeSet<>();
```

The rest of your code that uses `brands` doesn't need to change because it only  
expects a `Set`.  


## Example I

The following example creates a `HashSet`, determines its size, and prints all  
elements to the console.  

```java
import java.util.HashSet;
import java.util.Set;

void main() {

    Set<String> brands = new HashSet<>();

    brands.add("Wilson");
    brands.add("Nike");
    brands.add("Volvo");
    brands.add("IBM");
    brands.add("IBM");

    int nOfElements = brands.size();

    System.out.format("The set contains %d elements%n", nOfElements);
    System.out.println(brands);
}
```

In the code example, we have create a `HashSet` of brands. Each brand must be  
unique. For instance, there cannot be two IBM companies registered.  

```java
brands.add("IBM");
brands.add("IBM");
```

Even thought we try to add a brand two times, a set contains only one IBM brand.  

```java
int nOfElements = brands.size();
```

We determine the size of the brands set.

```java
System.out.println(brands);
```

All elements are printed to the console.


## Example II

In the following example, we present `add`, `remove`, `removeAll`, and `isEmpty`  
methods.  

```java
import java.util.HashSet;
import java.util.Set;

void main() {

    Set<String> brands = new HashSet<>();

    brands.add("Wilson");
    brands.add("Nike");
    brands.add("Volvo");
    brands.add("Kia");
    brands.add("Lenovo");

    Set<String> brands2 = new HashSet<>();

    brands2.add("Wilson");
    brands2.add("Nike");
    brands2.add("Volvo");

    System.out.println(brands);

    brands.remove("Kia");
    brands.remove("Lenovo");

    System.out.println(brands);

    brands.removeAll(brands2);

    System.out.println(brands);

    if (brands.isEmpty()) {

        System.out.println("The brands set is empty");
    }
}
```

The example builds a `HashSet` of brands and removes elements from it.

```java
System.out.println(brands);
```

The initial `HashSet` is printed to the console.

```java
brands.remove("Kia");
brands.remove("Lenovo");
```

```
System.out.println(brands);
```

We remove two elements with `remove` and print the contents of brands to the  
console.  

```java
brands.removeAll(brands2);
```

```java
System.out.println(brands);
```

Finally, we remove all elements contained in the second set from the first set.

```java
if (brands.isEmpty()) {

    System.out.println("The brands set is empty");
}
```

If the brands set is empty, we print a message to the terminal.


## Example III

In the following example, we use `add`, `contains`, `clear`, and `isEmpty`  
methods.  

```java
import java.util.HashSet;
import java.util.Set;

void main() {

    Set<String> brands = new HashSet<>();

    brands.add("Wilson");
    brands.add("Nike");
    brands.add("Volvo");
    brands.add("Kia");
    brands.add("Lenovo");

    if (brands.contains("Wilson")) {

        System.out.println("The set contains the Wilson element");
    } else {

        System.out.println("The set does not contain the Wilson element");
    }

    if (brands.contains("Apple")) {

        System.out.println("The set contains the Apple element");
    } else {

        System.out.println("The set does not contain the Apple element");
    }

    brands.clear();

    if (brands.isEmpty()) {

        System.out.println("The set does not contain any elements.");
    }
}
```

In the example, we check if two elements are present in the set.  

```java
if (brands.contains("Wilson")) {

    System.out.println("The set contains the Wilson element");
} else {

    System.out.println("The set does not contain the Wilson element");
}
```

We check if "Wilson" brand is present in the set and print a message  
accordingly.  

## HashSet iteration

We can use `forEach` method to iterate over the elements of the `HashSet`. The  
`forEach` method performs the given action for each element of the set until all  
elements have been processed or the action throws an exception.  

```java
import java.util.HashSet;
import java.util.Set;

void main() {

    Set<String> brands = new HashSet<>();

    brands.add("Wilson");
    brands.add("Nike");
    brands.add("Volvo");
    brands.add("Kia");
    brands.add("Lenovo");

    brands.forEach(e -> System.out.println(e));
}
```

With `forEach` method, we iterate over the set and print its elements to the  
console.  

Iterator is an object used to iterate over a collection. The iterator is  
retrieved with iterator.  

```java
import java.util.HashSet;
import java.util.Iterator;
import java.util.Set;

void main() {

    Set<String> brands = new HashSet<>();

    brands.add("Wilson");
    brands.add("Nike");
    brands.add("Volvo");
    brands.add("Kia");
    brands.add("Lenovo");

    Iterator<String> it = brands.iterator();

    while (it.hasNext()) {

        String element = it.next();
        System.out.println(element);
    }
}
```

The code example iterates over all elements of `HashSet` and prints them to the  
console.  

Enhanced for loop can be used to iterate over a `HashSet`.  

```java
import java.util.HashSet;
import java.util.Set;

void main() {

    Set<String> brands = new HashSet<>();

    brands.add("Wilson");
    brands.add("Nike");
    brands.add("Volvo");
    brands.add("Kia");
    brands.add("Lenovo");

    for (String brand: brands) {

        System.out.println(brand);
    }
}
```

In the example, we iterate over a `HashSet` with enhanced for loop.

```java
for (String brand: brands) {

    System.out.println(brand);
}
```

In each for cycle, a new element is assigned to the brand variable.
