# Parsing args with JCommander


`Main.java`:  

```java
package com.zetcode;

import com.beust.jcommander.Parameter;

public class Args {

    @Parameter(names = {"-n", "-now"}, description = "current datetime")
    private boolean showDateTime = false;

    @Parameter(names = {"-l", "-list"},  description = "list directory contents")
    private String directory;

    public boolean isShowDateTime() {
        return showDateTime;
    }

    public String getDirectory() {
        return this.directory;
    }
}
```

`Program.java`

```java
package com.zetcode;

import com.beust.jcommander.JCommander;
import com.beust.jcommander.ParameterException;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.time.Instant;

public class Program {

    Args args = new Args();

    public void run(String[] cmdArgs) {


        parseArgs(cmdArgs);

        if (args.getDirectory() != null) {

            listDirectory(args.getDirectory());
        }

        if (args.isShowDateTime()) {

            showCurrentDatetime();
        }
    }

    private void parseArgs(String[] cmdArgs) {
        try {
            JCommander.newBuilder()
                    .addObject(args)
                    .build()
                    .parse(cmdArgs);

        } catch (ParameterException ex) {
            System.out.println("invalid parameter");
            System.exit(1);
        }
    }

    private void showCurrentDatetime() {

        Instant now = Instant.now();
        System.out.println(now);
    }

    private void listDirectory(String dirName) {

        Path path = Path.of(dirName);

        try {
            try (var files = Files.list(path)) {

                files.forEach(System.out::println);
            }

        } catch (IOException e) {
            throw new RuntimeException(e);
        }

    }
}
```



