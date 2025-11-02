# CompletableFuture


## Get title 

```java
import org.jsoup.Jsoup;
import java.util.concurrent.CompletableFuture;

void main() {

  CompletableFuture.supplyAsync(() -> {
    try {
      return Jsoup.connect("https://example.com")
          .userAgent("Java HttpClient")
          .get()
          .title();
    } catch (Exception e) {
      throw new RuntimeException(e);
    }
  })
  .thenAccept(title -> IO.println("Page title: " + title))
  .exceptionally(ex -> {
    IO.println("Failed to fetch the page: " + ex.getMessage());
    return null;
  });

  // Simple wait for demo
  try {
    Thread.sleep(3000);
  } catch (InterruptedException e) {
    Thread.currentThread().interrupt();
  }
}
```

## Get title with join

```java
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.net.URI;
import java.util.concurrent.CompletableFuture;
import java.util.regex.Pattern;
import java.util.regex.Matcher;

void main() {

  HttpClient client = HttpClient.newHttpClient();
  HttpRequest request = HttpRequest.newBuilder()
      .uri(URI.create("https://example.com"))
      .GET()
      .build();

  CompletableFuture<Void> future = CompletableFuture.supplyAsync(() -> {
    try {
      HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
      String html = response.body();
      Pattern pattern = Pattern.compile("<title>(.*?)</title>", Pattern.CASE_INSENSITIVE);
      Matcher matcher = pattern.matcher(html);
      if (matcher.find()) {
        return matcher.group(1);
      } else {
        throw new RuntimeException("Title not found");
      }
    } catch (Exception e) {
      throw new RuntimeException(e);
    }
  })
  .thenAccept(title -> IO.println("Page title: " + title))
  .exceptionally(ex -> {
    IO.println("Failed to fetch the page: " + ex.getMessage());
    return null;
  });

  // Wait for the async task to complete
  future.join();

  IO.println("Done");
}
```

## Get title with regex

JSoup not used. 

```java
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.net.URI;
import java.util.concurrent.CompletableFuture;
import java.util.regex.Pattern;
import java.util.regex.Matcher;

void main() {

  HttpClient client = HttpClient.newHttpClient();
  HttpRequest request = HttpRequest.newBuilder()
      .uri(URI.create("https://example.com"))
      .GET()
      .build();

  CompletableFuture<Void> future = CompletableFuture.supplyAsync(() -> {
    try {
      HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
      String html = response.body();
      Pattern pattern = Pattern.compile("<title>(.*?)</title>", Pattern.CASE_INSENSITIVE);
      Matcher matcher = pattern.matcher(html);
      if (matcher.find()) {
        return matcher.group(1);
      } else {
        throw new RuntimeException("Title not found");
      }
    } catch (Exception e) {
      throw new RuntimeException(e);
    }
  })
  .thenAccept(title -> IO.println("Page title: " + title))
  .exceptionally(ex -> {
    IO.println("Failed to fetch the page: " + ex.getMessage());
    return null;
  });

  // Wait for the async task to complete
  future.join();

  IO.println("Done");
}
```

## 

```java
package com.zetcode;

import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.TimeUnit;
import java.util.function.BinaryOperator;
import java.util.function.Supplier;

class NewWord implements Supplier<String> {

    @Override
    public String get() {
        try {
            TimeUnit.SECONDS.sleep(2);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        return "deep sky";
    }
}

// we combine an completed future with an async task
// the two results are passed as arguments to the supplied function (transform)

public class CombineCompletedWithAsyncFuture {

    public static void main(String[] args) throws ExecutionException, InterruptedException {

        CompletableFuture<String> startValue = CompletableFuture.completedFuture("deep ocean");
        CompletableFuture<String> future = CompletableFuture.supplyAsync(new NewWord());

        BinaryOperator<String> transform = (f, s) -> f.toUpperCase() + "  " + s.toUpperCase();
        CompletableFuture<String> combinedFuture = future.thenCombine(startValue, transform);

        var result = combinedFuture.get();
        System.out.println(result);
    }
}
```

##

```java
package com.zetcode;

import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;

// runAfterEitherAsync returns a future which runs an async task
// when either of the supplied futures completes

public class RunAfterEitherAsync {

    public static void main(String[] args) throws InterruptedException {

        List<String> results = new ArrayList<>();

        CompletableFuture<Void> future1 = CompletableFuture.runAsync(() -> {
            try {
                TimeUnit.SECONDS.sleep(3);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            results.add("deep forest");
        });

        CompletableFuture<Void> future2 = CompletableFuture.runAsync(() -> {
            try {
                TimeUnit.SECONDS.sleep(5);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            results.add("blue sky");
        });

        CompletableFuture<Void> finisher = future1.runAfterEitherAsync(future2,
                () -> System.out.println(results));

        System.out.println(finisher.isDone());

        TimeUnit.SECONDS.sleep(8);

        System.out.println(finisher.isDone());
    }
}
```

## Get Multiple website statuses

```java
package com.zetcode;

import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.time.Duration;
import java.util.List;
import java.util.concurrent.CompletableFuture;
import java.util.stream.Stream;

import static java.util.stream.Collectors.toList;

public class WebSiteStatus {

    public static void main(String[] args) {

        List<URI> uris = Stream.of(
                "https://www.google.com/",
                "https://clojure.org",
                "https://www.rust-lang.org",
                "https://golang.org",
                "https://www.python.org",
                "https://code.visualstudio.com",
                "https://ifconfig.me",
                "http://termbin.com",
                "https://www.github.com/"
        ).map(URI::create).collect(toList());

        HttpClient httpClient = HttpClient.newBuilder()
                .connectTimeout(Duration.ofSeconds(10))
                .followRedirects(HttpClient.Redirect.ALWAYS)
                .build();

        var futures = uris.stream()
                .map(uri -> verifyUri(httpClient, uri))
                .toArray(CompletableFuture[]::new);

        CompletableFuture.allOf(futures).join();
    }

    private static CompletableFuture<Void> verifyUri(HttpClient httpClient,
                                                     URI uri) {
        HttpRequest request = HttpRequest.newBuilder()
                .timeout(Duration.ofSeconds(5))
                .uri(uri)
                .build();

        return httpClient.sendAsync(request, HttpResponse.BodyHandlers.discarding())
                .thenApply(HttpResponse::statusCode)
                .thenApply(statusCode -> statusCode == 200)
                .exceptionally(ex -> false)
                .thenAccept(valid -> {
                    if (valid) {
                        System.out.printf("[SUCCESS] Verified %s%n", uri);
                    } else {
                        System.out.printf("[FAILURE] Failed to verify%s%n", uri);
                    }
                });
    }
}
```

## 

```java
package com.zetcode;

import java.util.Random;
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;
import java.util.function.Function;
import java.util.function.Supplier;

public class TheyApply {

     // A random supplier that sleeps for a second, and then returns
     // a random value
    public static class RandomSupplier implements Supplier<Integer> {

        @Override
        public Integer get() {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            
            return new Random().nextInt(10);
        }
    }


    // A (pure) function that adds one to a given Integer
    public static class AddOne implements Function<Integer, Integer> {

        @Override
        public Integer apply(Integer x) {
            
            return x + 1;
        }
    }

    public static void main(String[] args) throws Exception {

        ExecutorService exec = Executors.newSingleThreadExecutor();

        CompletableFuture<Integer> future = CompletableFuture.supplyAsync(new RandomSupplier(), exec);
        System.out.println(future.isDone()); // false
        CompletableFuture<Integer> f2 = future.thenApply(new AddOne());
        System.out.println(f2.get()); // Waits until the "calculation" is done and prints the result

        exec.shutdown();

        try {
            if (!exec.awaitTermination(4, TimeUnit.SECONDS)) {
                exec.shutdownNow();
            }
        } catch (InterruptedException e) {
            exec.shutdownNow();
        }
    }
}
```

##  

```java
package com.zetcode;

import java.util.List;
import java.util.concurrent.CompletableFuture;
import java.util.stream.Collectors;
import java.util.stream.IntStream;

import static java.util.stream.Collectors.toList;

class Task {

    private final int duration;

    public Task(int duration) {
        this.duration = duration;
    }

    public int doTask() {
        System.out.printf("%s %n", Thread.currentThread().getName());

        try {
            Thread.sleep(duration * 1000);
        } catch (final InterruptedException e) {
            throw new RuntimeException(e);
        }

        return duration;
    }
}

public class RunTasksCompletableFuture {

    public static void main(String[] args) {

        long start = System.nanoTime();
        
        List<Task> tasks = IntStream.range(0, 10)
                .mapToObj(i -> new Task(1))
                .collect(toList());

        List<CompletableFuture<Integer>> futures =
                tasks.stream()
                        .map(task -> CompletableFuture.supplyAsync(task::doTask))
                        .collect(Collectors.toList());

        List<Integer> result =
                futures.stream()
                        .map(CompletableFuture::join)
                        .collect(Collectors.toList());

        long end = System.nanoTime();

        long duration = (end - start) / 1_000_000;

        System.out.printf("Run %d tasks in %d millis\n", tasks.size(), duration);
        System.out.println(result);
    }
}
```

