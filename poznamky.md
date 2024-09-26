# Java poznamky

Tento priklad ukazuje pouzitie pola.  

## Pole cisiel

```java
import java.util.Arrays;

void main() {

    int[] vals = {1, 2, 3, 4, 5, 6};

    // calculate sum
    int sum = 0;

    for (int val : vals) {
        sum += val;
    }

    System.out.println("The sum is: " + sum);

    int sum2 = Arrays.stream(vals).sum();
    System.out.println(sum2);

    // print first and last element

    System.out.println(vals[0]);
    System.out.println(vals[vals.length - 1]);

    // iterate array from the end

    for (int i=vals.length-1; i >= 0 ; i--) {

        System.out.println(vals[i]);
    }
}
```

## Hlavne okno

![IntelliJ Main](/images/intellij.png)


