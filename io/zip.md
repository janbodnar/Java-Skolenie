# ZipInputStream

`ZipInputStream` is a Java class that implements an input stream filter for  
reading files in the ZIP file format. It has support for both compressed and  
uncompressed entries.  

ZIP is an archive file format that supports lossless data compression. A ZIP  
file may contain one or more files or directories that may have been compressed.  
Java Archive (JAR) is built on the ZIP format.  


## Read ZIP example

The following example reads the contents of a ZIP file.  

```java
package com.zetcode;

import java.io.BufferedInputStream;
import java.io.FileInputStream;
import java.io.IOException;
import java.time.LocalDate;
import java.util.zip.ZipEntry;
import java.util.zip.ZipInputStream;

public class JavaReadZip {

    private final static Long MILLS_IN_DAY = 86400000L;

    public static void main(String[] args) throws IOException {

        String fileName = "src/resources/myfile.zip";

        try (FileInputStream fis = new FileInputStream(fileName);
                BufferedInputStream bis = new BufferedInputStream(fis);
                ZipInputStream zis = new ZipInputStream(bis)) {

            ZipEntry ze;

            while ((ze = zis.getNextEntry()) != null) {

                System.out.format("File: %s Size: %d last modified: %d",
                        ze.getName(), ze.getSize(),
                        LocalDate.ofEpochDay(ze.getTime() / MILLS_IN_DAY));
            }
        }
    }
}
```

The example reads the given ZIP file with `ZipInputStream` and prints its  
contents to the terminal. We print the file names, their size, and the last  
modification time.  

```java
try (FileInputStream fis = new FileInputStream(fileName);
```

We create a `FileInputStream` from the file. `FileInputStream` is used for  
reading streams of raw bytes.  

```java
BufferedInputStream bis = new BufferedInputStream(fis);
```

For better performance, we pass the `FileInputStream` into the  
`BufferedInputStream`.  

```java
ZipInputStream zis = new ZipInputStream(bis)) {
```

A `ZipInputStream` is created from the buffered `FileInputStream`. The  
try-with-resources closes the streams when they are not needed anymore.  

```java
while ((ze = zis.getNextEntry()) != null) {
```

In a while loop, we go through the entries of the ZIP file with `getNextEntry`
method. It returns null if there are no more entries.

```java
System.out.format("File: %s Size: %d last modified: %d",
    ze.getName(), ze.getSize(),
    LocalDate.ofEpochDay(ze.getTime() / MILLS_IN_DAY));
```

The `getName` returns the name of the entry, the `getSize` returns the  
uncompressed size of the entry, and the   `getTime` returns the last modification  
time of the entry.

## Decompress ZIP example

In the next example, we decompress a ZIP file in Java.

```java
package com.zetcode;

import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.zip.ZipEntry;
import java.util.zip.ZipInputStream;

public class JavaUnzip {

    public static void main(String args[]) throws Exception {

        byte[] buffer = new byte[2048];

        Path outDir = Paths.get("src/resources/output/");
        String zipFileName = "src/resources/myfile.zip";

        try (FileInputStream fis = new FileInputStream(zipFileName);
                BufferedInputStream bis = new BufferedInputStream(fis);
                ZipInputStream stream = new ZipInputStream(bis)) {

            ZipEntry entry;
            while ((entry = stream.getNextEntry()) != null) {

                Path filePath = outDir.resolve(entry.getName());

                try (FileOutputStream fos = new FileOutputStream(filePath.toFile());
                        BufferedOutputStream bos = new BufferedOutputStream(fos, buffer.length)) {

                    int len;
                    while ((len = stream.read(buffer)) > 0) {
                        bos.write(buffer, 0, len);
                    }
                }
            }
        }
    }
}
```

The example uses `ZipInputStream` to read the contents of the given ZIP file and  
`FileOutputStream` and `BufferedOutputStream` to write the contents into a  
directory.  

```java
Path outDir = Paths.get("src/resources/output/");
```

This is the directory where we extract the contents of the ZIP file.  

```java
while ((entry = stream.getNextEntry()) != null) {
```

In the first while loop, we go through the entries of the ZIP file.  

```java
while ((len  = stream.read(buffer)) > 0) {
    bos.write(buffer, 0, len);
}
```

In the second while loop, we read the entries and write them to the output  
stream.  


## Create a ZIP file

```java
import javax.swing.filechooser.FileSystemView;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.nio.file.DirectoryStream;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.nio.file.attribute.FileTime;
import java.util.zip.ZipEntry;
import java.util.zip.ZipOutputStream;


void createZip(String dirName, String destZipName) {

    Path directory = Paths.get(dirName);
    File zipFileName = Paths.get(destZipName).toFile();

    try (var zipStream = new ZipOutputStream(new FileOutputStream(zipFileName))) {

        try (DirectoryStream<Path> dirStream = Files.newDirectoryStream(directory)) {

            dirStream.forEach(path -> addToZipFile(path, zipStream));
        }

        System.out.printf("Zip file created in %s%n", directory.toFile().getPath());
    } catch (IOException | ZipParsingException e) {
        System.out.printf("failed to zip file. %s%n", e);
    }
}


void addToZipFile(Path file, ZipOutputStream zipStream) {

    String inputFileName = file.toFile().getPath();

    try (var inputStream = new FileInputStream(inputFileName)) {

        var entry = new ZipEntry(file.toFile().getName());
        entry.setCreationTime(FileTime.fromMillis(file.toFile().lastModified()));
        zipStream.putNextEntry(entry);

        System.out.printf("Generated new entry for: %s%n", inputFileName);

        byte[] readBuffer = new byte[2048];
        int amountRead;
        int written = 0;

        while ((amountRead = inputStream.read(readBuffer)) > 0) {
            zipStream.write(readBuffer, 0, amountRead);
            written += amountRead;
        }

        System.out.printf("Stored %d bytes to %s%n", written, inputFileName);


    } catch (IOException e) {
        throw new ZipParsingException("Unable to process %s".formatted(inputFileName) , e);
    }
}

void main() {

    String doc = FileSystemView.getFileSystemView().getDefaultDirectory().getPath();
    String srcDir = "%s/css".formatted(doc);
    String destZipName = "%s/css.zip".formatted(doc);

    System.out.println(doc);
    createZip(srcDir, destZipName);
}

class ZipParsingException extends RuntimeException {
    public ZipParsingException(String reason, Exception inner) {
        super(reason, inner);
    }
}
```
