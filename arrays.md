# Arrays

 An array is a container object that holds a fixed number of values of a single  
 type. The length of an array is established when the array is created. After  
 creation, its length is fixed.  

A scalar variable can hold only one item at a time. Arrays can hold multiple  
items. These items are called elements of the array. Arrays store data of the  
same data type. Each element can be referred to by an index. Arrays are zero  
based. The index of the first element is zero.  

```java
int[] ages;
String[] names;
float[] weights;
```

We have three array declarations. The declaration consists of two parts: the  
type of the array and the array name. The type of an array has a data type that  
determines the types of the elements within an array (int, String, float in our  
case) and a pair of square brackets `[]`. The brackets indicate that we have an  
array.

Collections serve a similar purpose like arrays. They are more powerful than  
arrays.  

## Initialization

```java
import java.util.Arrays;
 void main() {

    int[] a = new int[5];

    a[0] = 1;
    a[1] = 2;
    a[2] = 3;
    a[3] = 4;
    a[4] = 5;

    System.out.println(Arrays.toString(a));
}
```

---

```java
import java.util.Arrays;

void main() {

    // we can use var keyword
    var a = new int[] { 2, 4, 5, 6, 7, 3, 2 };

    System.out.println(Arrays.toString(a));
}
```

---

```java
import java.util.Arrays;

void main() {

    // here we cannot use var keyword
    int[] a = { 2, 4, 5, 6, 7, 3, 2 };

    System.out.println(Arrays.toString(a));
}
```

---

```java
import java.util.Arrays;

void main() {

    int[] a = new int[10];

    Arrays.fill(a, 1);

    System.out.println(Arrays.toString(a));

    int[] b = new int[10];

    Arrays.setAll(b, idx -> idx);

    System.out.println(Arrays.toString(b));
}
```

## Accessing elements

```java
void main(String[] args) {

    String[] names = {"Jane", "Thomas", "Lucy", "David"};

    System.out.println(names[0]);
    System.out.println(names[1]);
    System.out.println(names[2]);
    System.out.println(names[3]);
}
```

---

```java
import java.util.Arrays;

void main() {

    int[] vals = { 1, 2, 3 };

    vals[0] *= 2;
    vals[1] *= 2;
    vals[2] *= 2;

    System.out.println(Arrays.toString(vals));
}
```

## Traversing arrays

Using for loops.  

```java
void main() {

    String[] planets = { "Mercury", "Venus", "Mars", "Earth", "Jupiter",
            "Saturn", "Uranus", "Neptune", "Pluto" };

    for (int i = 0; i < planets.length; i++) {

        System.out.println(planets[i]);
    }

    for (String planet : planets) {

        System.out.println(planet);
    }
}
```

Using while loop. 

```java
void main() {

    String[] planets = { "Mercury", "Venus", "Mars", "Earth", "Jupiter",
            "Saturn", "Uranus", "Neptune", "Pluto" };

    int n = planets.length;
    int i = 0;

    while (i < n) {

        System.out.println(planets[i]);
        i++;
    }

    System.out.println("----------------------");


    int j = n - 1;

    while (j >= 0) {

        System.out.println(planets[j]);
        j--;
    }

}
```

Using `forEach` method. 

```java
import java.util.Arrays;

void main() {

    String[] planets = { "Mercury", "Venus", "Mars", "Earth", "Jupiter",
            "Saturn", "Uranus", "Neptune", "Pluto" };

    Arrays.stream(planets).forEach(System.out::println);
}
```

## Passing arrays to methods

```java
import java.util.Arrays;

void main() {

    int[] a = { 3, 4, 5, 6, 7 };
    int[] r = reverseArray(a);

    System.out.println(Arrays.toString(a));
    System.out.println(Arrays.toString(r));
}

int[] reverseArray(int[] b) {

    int[] c = new int[b.length];

    for (int i = b.length - 1, j = 0; i >= 0; i--, j++) {

        c[j] = b[i];
    }

    return c;
}
```

## Multidimensional arrays

So far we have been working with one-dimensional arrays. In Java, we can create  
multidimensional arrays. A multidimensional array is an array of arrays. In such  
an array, the elements are themselves arrays. In multidimensional arrays, we use  
two or more sets of brackets.  

Two-dimensional array:  

```java
void main() {

    int[][] twodim = new int[][] { { 1, 2, 3 }, { 1, 2, 3 } };

    int d1 = twodim.length;
    int d2 = twodim[1].length;

    for (int i = 0; i < d1; i++) {

        for (int j = 0; j < d2; j++) {

            System.out.println(twodim[i][j]);
        }
    }
}
```

---

```java
void main() {

    int[][][] n3 = {
            { { 12, 2, 8 }, { 0, 2, 1 } },
            { { 14, 5, 2 }, { 0, 5, 4 } },
            { { 3, 26, 9 }, { 8, 7, 1 } },
            { { 4, 11, 2 }, { 0, 9, 6 } }
    };

    int d1 = n3.length;
    int d2 = n3[0].length;
    int d3 = n3[0][0].length;

    for (int i = 0; i < d1; i++) {

        for (int j = 0; j < d2; j++) {

            for (int k = 0; k < d3; k++) {

                System.out.print(n3[i][j][k] + " ");
            }
        }
    }
}
```


## Irregular arrays

Arrays that have elements of the same size are called rectangular arrays. It is  
possible to create irregular arrays where the arrays have a different size. In  
C# such arrays are called jagged arrays.  


```java
void main() {

    int[][] ir = new int[][] {
            { 1, 2 },
            { 1, 2, 3 },
            { 1, 2, 3, 4 }
    };

    for (int[] a : ir) {
        for (int e : a) {
            System.out.print(e + " ");
        }
    }
}
```

## Array methods

The `Arrays` class, available in the `java.util` package, is a helper class that  
contains methods for working with arrays. These methods can be used for  
modifying, sorting, copying, or searching data. These methods that we use are  
static methods of the `Array` class. (Static methods are methods that can be  
called without creating an instance of a class.)  


```java
import java.util.Arrays;

void main() {

    int[] a = { 5, 2, 4, 3, 1 };

    Arrays.sort(a);

    System.out.println(Arrays.toString(a));

    Arrays.fill(a, 8);
    System.out.println(Arrays.toString(a));

    int[] b = Arrays.copyOf(a, 5);

    if (Arrays.equals(a, b)) {

        System.out.println("Arrays a, b are equal");
    } else {

        System.out.println("Arrays a, b are not equal");
    }
}
```

## Comparing arrays

There are two methods for comparing arrays. The `equals` method and the  
`deepEquals` method. The `deepEquals` method also compares references to arrays  
inside arrays.  

```java
import java.util.Arrays;

void main() {

    int[] a = { 1, 1, 2, 1, 1 };
    int[] b = { 0, 0, 3, 0, 0 };

    int[][] c = {
            { 1, 1, 2, 1, 1 },
            { 0, 0, 3, 0, 0 }
    };

    int[][] d = {
            a,
            b
    };

    System.out.print("equals() method: ");

    if (Arrays.equals(c, d)) {

        System.out.println("Arrays c, d are equal");
    } else {

        System.out.println("Arrays c, d are not equal");
    }

    System.out.print("deepEquals() method: ");

    if (Arrays.deepEquals(c, d)) {

        System.out.println("Arrays c, d are equal");
    } else {

        System.out.println("Arrays c, d are not equal");
    }
}
```

Now the `c` and `d` arrays are compared using both methods. For the `equals`  
method, the arrays are not equal. The `deepEquals` method goes deeper in the  
referenced arrays and retrieves their elements for comparison. For this method,  
the `c` and `d` arrays are equal.  


## Copy arrays


```java
import java.util.Arrays;

void main() {

    int[] vals = { 1, 2, 3, 4, 5, 6, 7, 8 };

    int[] vals2 = Arrays.copyOf(vals, 8);
    int[] vals3 = Arrays.copyOfRange(vals, 2, 7);

    // we need to create an empty array
    int[] vals4 = new int[8];
    System.arraycopy(vals, 0, vals4, 0, vals.length);

    System.out.println(Arrays.toString(vals));
    System.out.println(Arrays.toString(vals2));
    System.out.println(Arrays.toString(vals3));
    System.out.println(Arrays.toString(vals4));
}
```

## Array to String

```java
import java.util.Arrays;

void main() {

    int[] vals = { -1, 0, 1, 2, 3 };

    System.out.println(Arrays.toString(vals));
    // System.out.println(Arrays.deepToString(vals));

    int[][] a = {
            { 1, 1, 2, 1, 1 },
            { 0, 0, 3, 0, 0 }
    };

    System.out.println(Arrays.toString(a));
    System.out.println(Arrays.deepToString(a));
}
```

## Arrays.setAll

The `Arrays.setAll` set all elements of the specified array, using the provided  
generator function to compute each element.  


```java
import java.util.Arrays;

void main() {

    int[] a = new int[10];

    Arrays.setAll(a, idx -> idx);

    System.out.println(Arrays.toString(a));

    String[] vals = { "1", "2", "3", "4", "5" };

    int[] b = new int[vals.length];

    Arrays.setAll(b, idx -> Integer.parseInt(vals[idx]));

    System.out.println(Arrays.toString(b));
}
```


## Searching arrays

The `Arrays` class has a simple method for searching elements in an array. It is
called the `binarySearch`. The method searches for elements using a binary
search algorithm. The `binarySearch` method only works on sorted arrays.

```java
import java.util.Arrays;

void main() {

    String[] planets = { "Mercury", "Venus", "Mars", "Earth", "Jupiter",
            "Saturn", "Uranus", "Neptune", "Pluto" };

    Arrays.sort(planets);

    String p = "Earth";
    int r = Arrays.binarySearch(planets, p);

    String msg = "";

    if (r >= 0) {
        msg = STR."\{p} was found at position \{r} of the sorted array";
    } else {
        msg = STR."\{p} was not found";
    }

    System.out.println(msg);
}
```

In the example, we search for the "Earth" string in an array of planets.


## Download image


```java
import java.io.FileOutputStream;
import java.io.IOException;
import java.net.URI;
import java.net.URISyntaxException;

void main() throws IOException, URISyntaxException {

    String imageUrl = "https://something.com/favicon.ico";
    String destinationFile = "favicon.ico";

    var url = new URI(imageUrl).toURL();

    try (var is = url.openStream();
            var fos = new FileOutputStream(destinationFile)) {

        byte[] buf = new byte[1024];
        int noOfBytes;

        while ((noOfBytes = is.read(buf)) != -1) {

            fos.write(buf, 0, noOfBytes);
        }
    }
}
```


## Files.readAllBytes

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

// An array of bytes is used to store data 
// read from a file

void main() throws IOException {

    var fileName = "thermopylae.txt";
    var filePath = Paths.get(fileName);

    byte[] data = Files.readAllBytes(filePath);
    var content = new String(data);

    System.out.println(content);
}
```

## Hex output

```java

import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;

// the example reads a binary image into an array of bytes
// and write the bytes in hexadecimal format to the terminal

void main() throws IOException {

    var fileName = "ball.png";

    try (InputStream is = new FileInputStream(fileName)) {

        byte[] buffer = new byte[is.available()];
        is.read(buffer);

        int i = 0;

        for (byte b : buffer) {

            if (i % 10 == 0) {

                System.out.println();
            }

            System.out.printf("%02x ", b);

            i++;
        }
    }

    System.out.println();
}
```

## Sorting 

```java

import java.util.Arrays;

// Sorting an array of primitive integer values

public static void main(String[] args) {

    var nums = new int[] { 3, 2, 8, 1, 7, 0, 5, 4, 6 };

    Arrays.sort(nums);

    System.out.println(Arrays.toString(nums));

    for (int start = 0, end = nums.length - 1; start <= end; start++, end--) {

        int temp = nums[start];
        nums[start] = nums[end];
        nums[end] = temp;
    }

    System.out.println(Arrays.toString(nums));
}
```

---

```java
import java.util.Arrays;
import java.util.Comparator;

// Sorting an array of wrapper integer values

void main() {

    Integer[] vals = { 3, 2, 12, 5, 7, 12, 87, 43, 21, 12, 4 };

    Arrays.sort(vals, Comparator.naturalOrder());
    System.out.println(Arrays.toString(vals));

    Arrays.sort(vals, Comparator.reverseOrder());
    System.out.println(Arrays.toString(vals));
}
```


## List to array

```java
import java.util.Arrays;
import java.util.List;

void main() {

    List<Double> vals = List.of(2.3, 2.5, 3.1, 6.7);

    Double[] vals2 = vals.toArray(new Double[0]);
    System.out.println(Arrays.toString(vals2));

    double[] vals3 = vals.stream().mapToDouble(Double::doubleValue).toArray();
    System.out.println(Arrays.toString(vals3));
}
```

## Arrays.spliterator

```java

import java.util.Arrays;
import java.util.Spliterator;
import java.util.function.IntConsumer;

// split iterator gives read-only access to a range 
// of elements
void main(String[] args) {

    int[] vals = { 1, 2, 3, 4, 5, 6, 7, 8 };

    Spliterator.OfInt sit = Arrays.spliterator(vals, 2, 6);

    sit.forEachRemaining((IntConsumer) System.out::println);
}
```

## Vowels & consonants

```java
// count the number of vowels and consonants in 
// all words of a list
public static void main(String[] args) {

    String[] words = { "sun", "forest", "wood", "rocks" };

    int vowels = 0;
    int consonants = 0;

    for (int i = 0; i < words.length; i++) {

        String word = words[i];

        for (int j = 0; j < word.length(); j++) {

            char c = word.charAt(j);

            if (c == 'a' || c == 'e' || c == 'y' || c == 'i' || c == 'u' || c == 'o') {
                vowels++;
            } else {
                consonants++;
            }
        }
    }

    System.out.printf("Vowels: %d%n", vowels);
    System.out.printf("Consonants: %d%n", consonants);
}
```


