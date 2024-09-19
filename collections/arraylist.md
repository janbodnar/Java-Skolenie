# ArrayList


`ArrayList` is an ordered sequence of elements. It is dynamic and resizable. It  
provides random access to its elements. Random access means that we can grab any  
element at constant time. An `ArrayList` automatically expands as data is added.  
Unlike simple arrays, an `ArrayList` can hold data of multiple data types. It  
permits all elements, including `null`.  

Elements in the `ArrayList` are accessed via an integer index. Indexes are  
zero-based. Indexing of elements and insertion and deletion at the end of the  
`ArrayList` takes constant time.  

An `ArrayList` instance has a capacity. The capacity is the size of the array  
used to store the elements in the list. As elements are added to an `ArrayList`,  
its capacity grows automatically. Choosing a proper capacity can save some time.  

## Initialization 

It iss good practice to use the interface (`List`) on the left side of an  
assignment for flexibility:

```java
List<String> items = new ArrayList<>();
```

This approach allows you to change the implementation without affecting other  
parts of your code. For example, you can switch from `ArrayList` to `LinkedList`  
if you need better performance for frequent insertions and deletions:  

```java
List<String> items = new LinkedList<>();
```

The rest of your code remains unchanged because it interacts with the `List`  
interface, not directly with the implementation.  


## The add method

Single elements can be added to an `ArrayList` with the `add` method.

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    List<String> langs = new ArrayList<>();

    langs.add("Java");
    langs.add("Python");
    langs.add(1, "C#");
    langs.add(0, "Ruby");

    for (String lang : langs) {

        System.out.printf("%s ", lang);
    }

    System.out.println();
}
```

The example adds elements to an array list one by one.

```java
List<String> langs = new ArrayList<>();
```

An `ArrayList` is created. The data type specified inside the diamond brackets  
`<>` restricts the elements to this data type; in our case, we have a list of
strings.  

```java
langs.add("Java");
```

An element is appended at the end of the list with the `add` method.

```java
langs.add(1, "C#");
```

This time the overloaded add method inserts the element at the specified  
position; The "C#" string will be located at the second position of the list;  
remember, the ArrayList is an ordered sequence of elements.  

```java
for (String lang : langs) {

    System.out.printf("%s ", lang);
}
```

With the for loop, we go through the `ArrayList` list and print its elements.


## The List.of method

We have a couple of factory methods for creating lists having a handful of  
elements. The created list is immutable.  

```java
import java.util.List;

void main() {

    var words = List.of("wood", "forest", "falcon", "eagle");
    System.out.println(words);

    var values = List.of(1, 2, 3);
    System.out.println(values);
}
```

In the example, we create two lists that have four and three elements.

## The get and size methods

The get returns the element at the specified position in this list and the size  
returns the size of the list.  

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    List<String> colours = new ArrayList<>();

    colours.add("blue");
    colours.add("orange");
    colours.add("red");
    colours.add("green");

    String col = colours.get(1);
    System.out.println(col);

    int size = colours.size();

    System.out.printf("The size of the ArrayList is: %d%n", size);
}
```

The example uses the get and size methods of the `ArrayList`

```java
String col = colours.get(1);
```

The get method returns the second element, which is "orange".

```java
int size = colours.size();
```

The `size` method determines the size of our colours list; we have four elements.


## The copy method

A copy of a list can be generated with `List.copy` method.

```java
import java.util.List;

void main() {

    var words = List.of("forest", "wood", "eagle", "sky", "cloud");
    System.out.println(words);

    var words2 = List.copyOf(words);
    System.out.println(words2);
}
```

The example creates a copy of a list with `List.copy`.

## Raw ArrayList

An `ArrayList` can contain various data types. These are called raw lists.

Note: It is generally not recommended to use raw lists.  
Raw lists often require casts and they are not type safe.  

```java
import java.util.ArrayList;
import java.util.List;

class Base {}

enum Level {

    EASY,
    MEDIUM,
    HARD
}

void main() {

    Level level = Level.EASY;

    List da = new ArrayList();

    da.add("Java");
    da.add(3.5);
    da.add(55);
    da.add(new Base());
    da.add(level);

    for (Object el : da) {

        System.out.println(el);
    }
}
```

The example adds five different data types into an array list — a string,  
double, integer, object, and enumeration.  

```java
List da = new ArrayList();
```

When we add multiple data types to a list, we omit the angle brackets.


## The addAll method

The following example uses the `addAll` method to add multiple elements to a  
list in one step.  

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    List<String> colours1 = new ArrayList<>();

    colours1.add("blue");
    colours1.add("red");
    colours1.add("green");

    List<String> colours2 = new ArrayList<>();

    colours2.add("yellow");
    colours2.add("pink");
    colours2.add("brown");

    List<String> colours3 = new ArrayList<>();
    colours3.add("white");
    colours3.add("orange");

    colours3.addAll(colours1);
    colours3.addAll(2, colours2);

    for (String col : colours3) {

        System.out.println(col);
    }
}
```

Two lists are created. Later, the elements of the lists are added to the third  
list with the `addAll` method.  

```java
colours3.addAll(colours1);
```

The `addAll` method adds all of the elements to the end of the list.  

```java
colours3.addAll(2, colours2);
```

This overloaded method adds all of the elements starting at the specified  
position.  


## Modifying elements

The next example uses methods to modify the `ArrayList`.

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    List<String> items = new ArrayList<>();
    fillList(items);

    items.set(3, "watch");
    items.add("bowl");
    items.remove(0);
    items.remove("pen");

    for (Object el : items) {

        System.out.println(el);
    }

    items.clear();

    if (items.isEmpty()) {

        System.out.println("The list is empty");
    } else {
        System.out.println("The list is not empty");
    }
}

void fillList(List<String> data) {

    data.add("coin");
    data.add("pen");
    data.add("pencil");
    data.add("clock");
    data.add("book");
    data.add("spectacles");
    data.add("glass");
}
```

An `ArrayList` is created and modified with the `set`, `add`, `remove`, and  
`clear` methods.

```java
items.set(3, "watch");
```

The `set` method replaces the fourth element with the "watch" item.

```java
items.add("bowl");
```

The `add` method adds a new element at the end of the list.

```java
items.remove(0);
```

The `remove` method removes the first element, having index 0.

```java
items.remove("pen");
```

The overloaded `remove` method remove the first occurrence of the "pen" item.

```java
items.clear();
```

The `clear` method removes all elements from the list.

```java
if (items.isEmpty()) {
```

The `isEmpty` method determines if the list is empty.


## The removeIf method

The `removeIf` method removes all of the elements of a collection that satisfy  
the given predicate.  

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    List<Integer> values = new ArrayList<>();
    values.add(5);
    values.add(-3);
    values.add(2);
    values.add(8);
    values.add(-2);
    values.add(6);

    values.removeIf(val -> val < 0);

    System.out.println(values);
}
```

In our example, we have an `ArrayList` of integers. We use the `removeIf` method   
to delete all negative values.

```java
values.removeIf(val -> val < 0);
```

All negative numbers are removed from the array list.


## The removeAll method

The `removeAll` method removes from this list all of its elements that are  
contained in the specified collection. Note that all elements are removed with  
clear.  

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

void main() {

    List<String> letters = new ArrayList<>();
    letters.add("a");
    letters.add("b");
    letters.add("c");
    letters.add("a");
    letters.add("d");

    System.out.println(letters);

    letters.removeAll(Collections.singleton("a"));
    System.out.println(letters);
}
```

In the example, we remove all "a" letters from the list.

## The replaceAll method

The `replaceAll` method replaces each element of a list with the result of  
applying the operator to that element.  

```java
import java.util.ArrayList;
import java.util.List;
import java.util.function.UnaryOperator;

void main() {

    List<String> items = new ArrayList<>();
    items.add("coin");
    items.add("pen");
    items.add("cup");
    items.add("notebook");
    items.add("class");

    UnaryOperator<String> uo = (x) -> x.toUpperCase();

    items.replaceAll(uo);

    System.out.println(items);
}
```

The example applies an operator on each of the list elements; the elements'  
letters are transformed to uppercase.  

```java
UnaryOperator<String> uo = (x) -> x.toUpperCase();
```

A `UnaryOperator` that transforms letters to uppercase is created.

```java
items.replaceAll(uo);
```

The operator is applied on the list elements with the `replaceAll` method.  

The second example uses the `replaceAll` method to capitalize string items.  

```java
import java.util.ArrayList;
import java.util.List;
import java.util.function.UnaryOperator;

class MyOperator<T> implements UnaryOperator<String> {

    @Override
    public String apply(String s) {

        if (s == null || s.length() == 0) {
            return s;
        }

        return s.substring(0, 1).toUpperCase() + s.substring(1);
    }
}

void main() {

    List<String> items = new ArrayList<>();

    items.add("coin");
    items.add("pen");
    items.add("cup");
    items.add("notebook");
    items.add("glass");

    items.replaceAll(new MyOperator<>());

    System.out.println(items);
}
```

We have a list of string items. These items are capitalized with the help of the  
`replaceAll` method.  

```java
class MyOperator<T> implements UnaryOperator<String> {
```

A custom `UnaryOperator` is created.

```java
@Override
public String apply(String s) {

    if (s == null || s.length() == 0) {
        return s;
    }

    return s.substring(0, 1).toUpperCase() + s.substring(1);
}
```

Inside the `UnaryOperator's` `apply` me  thod, we retur the string with its first  
letter in uppercase.

```java
items.replaceAll(new MyOperator<>());
```

The operator is applied on the list items.

## The contains method

The `contains` method returns true if a list contains the specified element.  

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    List<String> items = new ArrayList<>();

    items.add("coin");
    items.add("pen");
    items.add("cup");
    items.add("notebook");
    items.add("class");

    String item = "pen";

    if (items.contains(item)) {

        System.out.printf("There is a %s in the list%n", item);
    }
}
```

The example checks if the specified item is in the list.

```java
if (items.contains(item)) {

    System.out.printf("There is a %s in the list%n", item);
}
```

The message is printed if the item is in the list.  


## Getting index of elements

Each of the elements in an ArrayList has its own index number. The `indexOf`  
returns the index of the first occurrence of the specified element, or -1 if the  
list does not contain the element. The `lasindexOf` returns the index of the  
last occurrence of the specified element, or -1 if the list does not contain the  
element.  

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    List<String> colours = new ArrayList<>();

    colours.add(0, "blue");
    colours.add(1, "orange");
    colours.add(2, "red");
    colours.add(3, "green");
    colours.add(4, "orange");

    int idx1 = colours.indexOf("orange");
    System.out.println(idx1);

    int idx2 = colours.lastIndexOf("orange");
    System.out.println(idx2);
}
```

The example prints the first and last index of the "orange" element.

## List of lists

We can add other lists into a list.

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    List<Integer> l1 = new ArrayList<>();
    l1.add(1);
    l1.add(2);
    l1.add(3);

    List<Integer> l2 = new ArrayList<>();
    l2.add(4);
    l2.add(5);
    l2.add(6);

    List<Integer> l3 = new ArrayList<>();
    l3.add(7);
    l3.add(8);
    l3.add(9);

    List<List<Integer>> nums = new ArrayList<>();
    nums.add(l1);
    nums.add(l2);
    nums.add(l3);

    System.out.println(nums);

    for (List<Integer> list : nums) {

        for (Integer n : list) {

            System.out.printf("%d ", n);
        }

        System.out.println();
    }
}
```

The example creates three lists of integers. Later, the lists are added into
another fourth list.

```java
List<Integer> l1 = new ArrayList<>();
l1.add(1);
l1.add(2);
l1.add(3);
```

A list of integers is created.

```java
List<List> nums = new ArrayList<>();
nums.add(l1);
nums.add(l2);
nums.add(l3);
```

A list of lists is created.

```java
for (List<Integer> list : nums) {

    for (Integer n : list) {

        System.out.printf("%d ", n);
    }

    System.out.println();
}
```

We use two for loops to go through all the elements.


## The subList method

The `subList` method returns a view of the portion of a list between the  
specified fromIndex, inclusive, and toIndex, exclusive. The changes in a sublist  
are reflected in the original list.  

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    List<String> items = new ArrayList<>();

    items.add("coin");
    items.add("pen");
    items.add("cup");
    items.add("notebook");
    items.add("glass");
    items.add("chair");
    items.add("ball");
    items.add("bowl");

    List<String> items2 = items.subList(2, 5);

    System.out.println(items2);

    items2.set(0, "bottle");

    System.out.println(items2);
    System.out.println(items);
}
```

The example creates a sublist from a list of items.

```java
List<String> items2 = items.subList(2, 5);
```

A `sublist` is created with the `subList` method; it contains items with indexes
2, 3, and 4.

```java
items2.set(0, "bottle");
```

We replace the first item of the `sublist`; the modification is reflected in the  
original list, too.  


## Traversing elements

In the following example, we show five ways to traverse an `ArrayList`.

```java
import java.util.ArrayList;
import java.util.List;
import java.util.ListIterator;

void main() {

    List<Integer> nums = new ArrayList<>();
    nums.add(2);
    nums.add(6);
    nums.add(7);
    nums.add(3);
    nums.add(1);
    nums.add(8);

    for (int i = 0; i < nums.size(); i++) {

        System.out.printf("%d ", nums.get(i));
    }

    System.out.println();

    for (int num : nums) {

        System.out.printf("%d ", num);
    }

    System.out.println();

    int j = 0;
    while (j < nums.size()) {

        System.out.printf("%d ", nums.get(j));
        j++;
    }

    System.out.println();

    ListIterator<Integer> it = nums.listIterator();

    while(it.hasNext()) {

        System.out.printf("%d ", it.next());
    }

    System.out.println();

    nums.forEach(e -> System.out.printf("%d ", e));
    System.out.println();
}
```

In the example, we traverse an array list of integers with for loops, while  
loop, iterator, and forEach construct.  

```java
List<Integer> nums = new ArrayList<>();
nums.add(2);
nums.add(6);
nums.add(7);
nums.add(3);
nums.add(1);
nums.add(8);
```

We have created an `ArrayList` of integers.

```java
for (int i = 0; i < nums.size(); i++) {

    System.out.printf("%d ", nums.get(i));
}
```

Here, we use the classic for loop to iterate over the list.

```java
for (int num : nums) {

    System.out.printf("%d ", num);
}
```

The second way uses the enhanced-for loop.

```java
int j = 0;

while (j < nums.size()) {

    System.out.printf("%d ", nums.get(j));
    j++;
}
```

The third way uses the while loop.

```java
ListIterator<Integer> it = nums.listIterator();

while(it.hasNext()) {

    System.out.printf("%d ", it.next());
}
```

Here, a `ListIterator` is used to traverse the list.

```java
nums.forEach(e -> System.out.printf("%d ", e));
```

In the last way, we use the `forEach` method.

## Sorting elements

There are different wasy to sort an `ArrayList`.

### Sorting with the sort method

The `ArrayList's` `sort` method sorts a list according to the order induced by  
the specified comparator.  

```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;


void main() {

    List<Person> persons = createList();
    persons.sort(Comparator.comparing(Person::age).reversed());

    System.out.println(persons);

}

List<Person> createList() {

    List<Person> persons = new ArrayList<>();

    persons.add(new Person(17, "Jane"));
    persons.add(new Person(32, "Peter"));
    persons.add(new Person(47, "Patrick"));
    persons.add(new Person(22, "Mary"));
    persons.add(new Person(39, "Robert"));
    persons.add(new Person(54, "Greg"));

    return persons;
}

record Person(int age, String name) {}
```

We have an `ArrayList` of custom `Person` classes. We sort the persons according  
to their age in a reversed order.  

```java
persons.sort(Comparator.comparing(Person::age).reversed());
```

This line sorts the persons by their age, from the oldest to the youngest.  


### Sorting elements using stream

In the second example, we use Java stream to sort the `ArrayList`. The `Stream`  
API allows a more powerful way to do sorting.  

```java
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;

void main() {

    List<Country> countries = createList();

    List<Country> sorted_countries = countries.stream()
            .sorted((e1, e2) -> Integer.compare(e1.population,
                    e2.population))
            .collect(Collectors.toList());

    System.out.println(sorted_countries);
}

List<Country> createList() {

    List<Country> countries = new ArrayList<>();

    countries.add(new Country("Slovakia", 5424000));
    countries.add(new Country("Hungary", 9845000));
    countries.add(new Country("Poland", 38485000));
    countries.add(new Country("Germany", 81084000));
    countries.add(new Country("Latvia", 1978000));

    return countries;
}

record Country(String name, int population) {
}
```

In this example, we have a list of countries. Each country has a name and  
population. The countries are sorted by population.  

```java
List<Country> sorted_countries = countries.stream()
        .sorted((e1, e2) -> Integer.compare(e1.population,
                e2.population))
        .collect(Collectors.toList());
```

With the `stream` method, we create a stream from a list. The `sorted` method  
sorts elements according to the provided comparator. With` Integer.compare` we  
compare the populations of countries. With `collect`, we transform the stream   
into a list of countries.  

The countries are sorted by their population in ascending mode.  

## Working with ArrayList and simple Java array

The following example uses an `ArrayList` with a simple Java array.

```java
import java.util.Arrays;
import java.util.List;

void main() {

    String[] a = new String[] { "Mercury", "Venus", "Earth",
            "Mars", "Jupiter", "Saturn", "Uranus", "Neptune" };

    List<String> planets = List.of(a);
    System.out.println(planets);

    String[] planets2 = planets.toArray(new String[0]);
    System.out.println(Arrays.toString(planets2));
}
```

An `ArrayList` is converted to an array and vice versa.

```java
String[] a = new String[] { "Mercury", "Venus", "Earth",
        "Mars", "Jupiter", "Saturn", "Uranus", "Neptune" };
```

We have an array of strings.

```java
List<String> planets = List.of(a);
```

We generate an immutable list from the array with `List.of`;

```java
String[] planets2 = planets.toArray(new String[0]);
```

The `ArrayList's` `toArray` is used to convert a list to an array.  

## Stream to list

Java streams can be converted to lists using collectors.  

```java
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.Stream;

void main() {

    var words = Stream.of("forest", "eagle", "river", "cloud", "sky");

    List<String> words2 = words.collect(Collectors.toList());
    System.out.println(words2.getClass());
}
```

We have a stream of strings. We convert the stream to a list with  
`Collectors.toList`.  
