# FileReader

`FileReader` is a Java convenience class for reading text files. `FileReader`  
extends `InputStreamReader` and creates the `FileInputStream`.  


```
The Battle of Thermopylae was fought between an alliance of
Greek city-states, led by King Leonidas of Sparta, and the Persian Empire of
Xerxes I over the course of three days, during the second Persian invasion of
Greece. 
```

The `thermopylae.txt` file.   


Note: In the past, `FileReader` relied on the default platform's encoding. Since  
Java 11, the issue was corrected. It is possible now to explicitly specify the  
encoding. Always specify the encoding when using `FileReader`.  


## The read method

In the following example, we use `FileReader's` read method to read a text file.  
It reads characters into an array. It will block until some input is available,  
an I/O error occurs, or the end of the stream is reached.  

```java
import java.io.FileReader;
import java.io.IOException;
import java.nio.charset.StandardCharsets;


void main() throws IOException {

    var fileName = "thermopylae.txt";
    char[] buf = new char[1024];

    try (var fr = new FileReader(fileName, StandardCharsets.UTF_8)) {

        int c;
        while ((c = fr.read(buf)) != -1) {

            System.out.println(buf);
        }
    }
}
```

The example reads a text file. It uses a character buffer to improve the  
performance of the operation.  

```java
try (var fr = new FileReader(fileName, StandardCharsets.UTF_8)) {
```

The first argument of the `FileReader` is the file name. The second is the  
encoding type. We use try-with-resources construct to clean resources after we  
have finished writing.  

```java
int c;
while ((c = fr.read(buf)) != -1) {

    System.out.println(buf);
}
```

The `FileReader's` read method reads characters into an array. It returns the  
the number of characters read, or `-1` if the end of the stream has been  
reached.  

## Reading with BufferedReader

`FileReader's` performance can be improved with `BufferedReader`.  
`BufferedReader` reads text from a character-input stream, buffering characters  
so as to provide for the efficient reading of characters, arrays, and lines. The  
buffer size may be specified, or the default size may be accepted; the default  
is large enough for most purposes.  

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.nio.charset.StandardCharsets;

void main() throws IOException {

    var fileName = "thermopylae.txt";

    try (var br = new BufferedReader(new FileReader(fileName,
            StandardCharsets.UTF_8))) {

        String line;
        while ((line = br.readLine()) != null) {

            System.out.println(line);
        }
    }
}
```

In the example, we wrap the `FileReader` into the `BufferedReader` to improve  
its performance.  

```java
String line;
while ((line = br.readLine()) != null) {

    System.out.println(line);
}
```

The `readLine` reads a line of text. It returns the string containing the  
contents of the line, not including any line-termination characters, or null if  
the end of the stream has been reached without reading any characters.  

## Count word frequency

In the following example, we count the frequency of words in the text file.  

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.HashMap;
import java.nio.charset.StandardCharsets;


void main() throws IOException {

    var fileName = "thermopylae.txt";
    var wordFreq = new HashMap<String, Integer>();

    try (var bufferedReader = new BufferedReader(new FileReader(fileName, 
            StandardCharsets.UTF_8))) {

        String line;
        while ((line = bufferedReader.readLine()) != null) {

            var words = line.split("\s");

            for (var word : words) {

                if (word.endsWith(",") || word.endsWith("?")
                    || word.endsWith("!") || word.endsWith(".")) {

                    word = word.substring(0, word.length()-1);
                }

                if (wordFreq.containsKey(word)) {
                    wordFreq.put(word, wordFreq.get(word) + 1);
                } else {
                    wordFreq.put(word, 1);
                }

            }
        }

        wordFreq.forEach((k, v) -> {
            System.out.printf("%s -> %d%n", k, v);
        });
    }
}
```

We read the file line by line and split the lines into words. Then we remove any  
possible commans, question marks, exclamation marks, or dots from the words. The  
frequencies of words are kept in a hashmap.  
