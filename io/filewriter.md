# FileWriter

`FileWriter` is a Java convenience class for writing text data to files.  
`FileWriter` extends `OutputStreamWriter` and creates the `FileOutputStream`.  

Note: In the past, `FileWriter` relied on the default platform's encoding. Since  
Java 11, the issue was corrected. It is possible now to explicitly specify the  
encoding. Always specify the encoding when using `FileWriter`.  

## FileWriter example

The following example writes a line to a file.

```java
import java.io.FileWriter;
import java.io.IOException;

void main(String[] args) throws IOException {

    var fileName = "src/resources/myfile.txt";

    try (var fr = new FileWriter(fileName, StandardCharsets.UTF_8)) {

        fr.write("Today is a sunny day");
    }
}
```

The example writes text data to a file with FileWriter.

```java
try (var fr = new FileWriter(fileName, StandardCharsets.UTF_8)) {
```

The first parameter of the `FileWriter` is the file name. The second is the  
encoding used. We use try-with-resources construct to clean resources after we  
have finished writing.  

```java
writer.write("Today is a sunny day");
```

The `FileWriter's` `write` method writes text to the file.  
  
## FileWriter append to file

With `FileWriter` it is possible to append text to a file. The typical usage for  
appending is logging.  

```java
import java.io.FileWriter;
import java.io.IOException;
import java.nio.charset.StandardCharsets;

void main() throws IOException {

    var fileName = "src/resources/myfile.txt";

    try (var fr = new FileWriter(fileName, StandardCharsets.UTF_8, true)) {

        fr.write("Tomorrow will be cloudy.");
    }
}
```

The code example appends text to file.

```java
try (var fr = new FileWriter(fileName, StandardCharsets.UTF_8, true)) {
```

The second parameter of `FileWriter` tells that we will append to the file.  

## FileWriter & BufferedWriter

`FileWriter's` performance can be improved with `BufferedWriter`.  
`BufferedWriter` writes text to a character-output stream, buffering characters  
to improve the performance of writing single characters, arrays, and strings.  
The buffer size may be specified, or the default size may be accepted; the  
default is large enough for most purposes.  

```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.URI;
import java.nio.charset.StandardCharsets;

void main() throws IOException {

    String text = readText();

    var fileName = "src/resources/webcode_home_page.txt";

    try (var fr = new FileWriter(fileName, StandardCharsets.UTF_8);
         var bufWriter = new BufferedWriter(fr)) {

        bufWriter.write(text);
    }
}

String readText() throws IOException {

    StringBuilder sb;

    var url = URI.create("https://webcode.me").toURL();

    try (var br = new BufferedReader(new InputStreamReader(url.openStream(),
            StandardCharsets.UTF_8))) {

        String line;
        sb = new StringBuilder();

        while ((line = br.readLine()) != null) {

            sb.append(line);
            sb.append(System.lineSeparator());
        }
    }

    return sb.toString();
}
```

In the example, we read webcode's home page (its HTML code) and write it to a  
file. The home page is large enough to consider buffering.  

```java
try (var fr = new FileWriter(fileName, StandardCharsets.UTF_8);
    var bufWriter = new BufferedWriter(fr)) {

   bufWriter.write(text);
}
```

The `FileWriter` is passed to the `BufferedWriter` as a parameter. Then we call  
the `BufferedWriter's` `write` method to write the text.  

```java
try (var br = new BufferedReader(new InputStreamReader(url.openStream(),
    StandardCharsets.UTF_8))) {
```

The reading operation is buffered as well with the `BufferedReader` class.

## Specifying encoding with pre-Java 11

A workaround with pre-Java 11 `FileWriter` encoding issue was to use the  
`OutputStreamWriter` and `FileOutputStream` instead.  

```java
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStreamWriter;
import java.nio.charset.StandardCharsets;

void main(String[] args) throws IOException {

    String fileName = "src/resources/myfile.txt";

    try (var osw = new OutputStreamWriter(new FileOutputStream(fileName),
            StandardCharsets.UTF_8)) {
        osw.write("Сегодня был прекрасный день.");
    }
}
```

The example writes text to a file with `OutputStreamWriter`. The second  
parameter is the charset to be used.  
