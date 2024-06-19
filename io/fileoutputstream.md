# FileOutputStream 

`FileOutputStream` is an output stream for writing data to a File or to a  
FileDescriptor. `FileOutputStream` is a subclass of OutputStream, which accepts  
output bytes and sends them to some sink. In case of `FileOutputStream`, the  
sink is a file object.  


## FileOutputStream close

The` FileOutputStream's` close method closes file output stream and releases any  
system resources associated with this stream. In our examples we use  
try-with-resources statement, which ensures that each resource is closed at the  
end of the statement.  

`FileOutputStream` writes bytes with the following write methods :

- `write(byte[] b)` — writes array of bytes to the file output stream.  
- `write(byte[] b, int off, int len)` — writes len bytes from the specified byte  
  array starting at offset off to the file output stream.  
- `write(int b)` — writes one byte to the file output stream.  

## FileOutputStream example

The following example uses `FileOutputStream` to write text to a file.  

```java
import java.io.FileOutputStream;
import java.io.IOException;

void main() throws IOException {

    String fileName = "src/resources/newfile.txt";

    try (var fos = new FileOutputStream(fileName)) {

        String text = "Today is a beautiful day";
        byte[] mybytes = text.getBytes();

        fos.write(mybytes);
    }
}
```

The code example writes one line to a file.

```java
try (var fos = new FileOutputStream(fileName)) {
```

The `FileOutputStream` constructor takes a string as a parameter; it is the file  
name to which we write. We use try-with-resources construct to clean resources  
after we have finished writing.  

```java
String text = "Today is a beautiful day";
byte[] mybytes = text.getBytes();
```

`FileOutputStream` write bytes to the file; we get bytes from a string with the
`getBytes` method.

```java
fos.write(mybytes);
```

The bytes are written to the file.


## FileOutputStream append to file

With `FileOutputStream` it is possible to append data to a file. The typical  
usage for appending is logging.  

```java
import java.io.FileOutputStream;
import java.io.IOException;

void main() throws IOException {

    String fileName = "src/resources/newfile.txt";

    try (var fos = new FileOutputStream(fileName, true)) {

        String text = "Today is a beautiful day";
        byte[] mybytes = text.getBytes();

        fos.write(mybytes);
    }
}
```

The code example appends text to file.

```java
try (var fos = new FileOutputStream(fileName, true)) {
```
 
The second parameter of `FileOutputStream` indicates that we will append to the  
file.  

## Specifying encoding

`FileWriter` class, which is a Java convenience class for writing character  
files, has a serious limitation: it uses the default encoding and does not allow  
us to explicitly specify the encoding. If we have to set the encoding, we can  
use `OutputStreamWriter` and `FileOutputStream`.  

```java
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStreamWriter;
import java.nio.charset.StandardCharsets;


void main() throws IOException {

    String fileName = "src/resources/newfile.txt";
    var fos = new FileOutputStream(fileName);
    
    try (var osw =  new OutputStreamWriter(fos, StandardCharsets.UTF_8)) {

        String text = "Сегодня был прекрасный день.";
        osw.write(text);
    }
}
```

The example writes text to a file with `OutputStreamWriter`. The second  
parameter is the charset to be used.  


## Copy file without a buffer 

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.nio.file.Path;
import java.nio.file.Paths;


void main(String[] args) throws IOException {
    
    Path inputPath = Paths.get("src/resources/bugs.txt");
    Path outputPath = Paths.get("src/resources/bugs2.txt");

    try (var fis = new FileInputStream(inputPath.toFile());
         var fos = new FileOutputStream(outputPath.toFile())) {

        int data;
        while ((data = fis.read()) != -1) {
            fos.write(data);
        }

        System.out.println("File copied successfully!");
    }
}
```


## Copy file using a buffer

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.nio.file.Path;
import java.nio.file.Paths;


void main(String[] args) throws IOException {

    Path inputPath = Paths.get("src/resources/bugs.txt");
    Path outputPath = Paths.get("src/resources/bugs2.txt");

    try (var fis = new FileInputStream(inputPath.toFile());
         var fos = new FileOutputStream(outputPath.toFile())) {

        byte[] buffer = new byte[1024];
        int bytesRead;

        while ((bytesRead = fis.read(buffer)) != -1) {
            fos.write(buffer, 0, bytesRead);
        }

        System.out.println("File copied successfully!");
    }
}
```
