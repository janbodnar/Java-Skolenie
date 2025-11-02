# CompletableFuture

`CompletableFuture` is a powerful class introduced in Java 8 that represents a  
future result of an asynchronous computation. It implements both the `Future`  
and `CompletionStage` interfaces, providing a rich API for composing,  
combining, and handling asynchronous operations in a functional style.

## Key Features

- **Asynchronous Execution**: Execute tasks asynchronously without blocking the  
  main thread, improving application responsiveness and throughput.

- **Composability**: Chain multiple asynchronous operations together using  
  methods like `thenApply`, `thenCompose`, and `thenCombine`, enabling complex  
  workflows with clean, readable code.

- **Exception Handling**: Handle exceptions gracefully with methods like  
  `exceptionally`, `handle`, and `whenComplete`, providing robust error  
  management in asynchronous pipelines.

- **Combining Multiple Futures**: Coordinate multiple asynchronous tasks using  
  `allOf` and `anyOf`, allowing parallel execution and aggregation of results.

- **Custom Executors**: Control thread execution by providing custom  
  `Executor` instances, enabling fine-grained control over concurrency.

- **Non-blocking**: Unlike traditional `Future`, `CompletableFuture` allows  
  registering callbacks that execute when the computation completes, avoiding  
  blocking calls.

## Core Concepts

### Creation Methods

- `supplyAsync(Supplier<U> supplier)`: Creates a CompletableFuture that  
  asynchronously completes with the result of the supplier function.

- `runAsync(Runnable runnable)`: Creates a CompletableFuture that runs an  
  asynchronous task without returning a result.

- `completedFuture(U value)`: Returns a CompletableFuture already completed  
  with the given value.

### Transformation Methods

- `thenApply(Function<T,U> fn)`: Transforms the result when the future completes.

- `thenAccept(Consumer<T> action)`: Performs an action with the result without  
  returning a new value.

- `thenRun(Runnable action)`: Runs an action after completion, ignoring the result.

### Combining Methods

- `thenCombine(CompletionStage<U> other, BiFunction<T,U,V> fn)`: Combines two  
  futures and applies a function to both results.

- `thenCompose(Function<T,CompletionStage<U>> fn)`: Chains dependent  
  asynchronous operations, similar to flatMap.

### Error Handling Methods

- `exceptionally(Function<Throwable,T> fn)`: Handles exceptions and provides a  
  fallback value.

- `handle(BiFunction<T,Throwable,U> fn)`: Handles both success and failure cases.

- `whenComplete(BiConsumer<T,Throwable> action)`: Performs an action when the  
  future completes, regardless of success or failure.

## Fetch Web Page Title Asynchronously

This example demonstrates using `supplyAsync` to fetch a web page title  
asynchronously with JSoup. The `thenAccept` method processes the result, while  
`exceptionally` handles any errors that occur during the fetch operation.

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

## Fetch Web Page Title with Join

This example shows how to use `join()` to wait for the asynchronous operation  
to complete. Unlike `get()`, `join()` throws an unchecked exception, making it  
more convenient in lambda expressions and streams. It uses Java's HttpClient  
and regex to extract the page title.

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

## Extract Title Using Regex Without JSoup

This example demonstrates fetching a web page and extracting the title using  
regex pattern matching instead of JSoup. It showcases pure Java approach using  
HttpClient for HTTP requests and Pattern/Matcher for HTML parsing.

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

## Combining Two Futures with thenCombine

This example demonstrates how to combine results from two separate  
CompletableFutures using `thenCombine`. It takes a completed future and an  
async future, then applies a transformation function to both results,  
converting them to uppercase and concatenating them.

```java

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
// the two results are passed as arguments to the supplied function
// (transform)

void main(String[] args)
    throws ExecutionException, InterruptedException {

  CompletableFuture<String> startValue = CompletableFuture
      .completedFuture("deep ocean");
  CompletableFuture<String> future = CompletableFuture
      .supplyAsync(new NewWord());

  BinaryOperator<String> transform = (f,
      s) -> f.toUpperCase() + "  " + s.toUpperCase();
  CompletableFuture<String> combinedFuture = future
      .thenCombine(startValue, transform);

  var result = combinedFuture.get();
  System.out.println(result);
}
```

## Run Action After Either Future Completes

This example uses `runAfterEitherAsync` to execute an action when either of two  
futures completes. It demonstrates racing two async tasks and performing an  
action as soon as the first one finishes, useful for implementing timeout  
patterns or fastest-response strategies.

```java

import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;

// runAfterEitherAsync returns a future which runs an async task
// when either of the supplied futures completes

public static void main(String[] args)
    throws InterruptedException {

  List<String> results = new ArrayList<>();

  CompletableFuture<Void> future1 = CompletableFuture
      .runAsync(() -> {
        try {
          TimeUnit.SECONDS.sleep(3);
        } catch (InterruptedException e) {
          e.printStackTrace();
        }
        results.add("deep forest");
      });

  CompletableFuture<Void> future2 = CompletableFuture
      .runAsync(() -> {
        try {
          TimeUnit.SECONDS.sleep(5);
        } catch (InterruptedException e) {
          e.printStackTrace();
        }
        results.add("blue sky");
      });

  CompletableFuture<Void> finisher = future1
      .runAfterEitherAsync(future2,
          () -> System.out.println(results));

  System.out.println(finisher.isDone());

  TimeUnit.SECONDS.sleep(8);

  System.out.println(finisher.isDone());
}
```

## Check Multiple Website Statuses Concurrently

This example demonstrates parallel verification of multiple website statuses  
using `allOf`. It creates multiple asynchronous HTTP requests and waits for all  
of them to complete, efficiently checking if websites are accessible with a  
200 status code.

```java
import module java.net.http;

void main() {
  List<URI> uris = Stream
      .of("https://www.google.com/", "https://clojure.org",
          "https://www.rust-lang.org", "https://golang.org",
          "https://www.python.org",
          "https://code.visualstudio.com",
          "https://ifconfig.me", "http://termbin.com",
          "https://www.github.com/")
      .map(URI::create).collect(Collectors.toList());

  HttpClient httpClient = HttpClient.newBuilder()
      .connectTimeout(Duration.ofSeconds(10))
      .followRedirects(HttpClient.Redirect.ALWAYS).build();

  var futures = uris.stream()
      .map(uri -> verifyUri(httpClient, uri))
      .toArray(CompletableFuture[]::new);

  CompletableFuture.allOf(futures).join();
}

CompletableFuture<Void> verifyUri(HttpClient httpClient,
    URI uri) {
  HttpRequest request = HttpRequest.newBuilder()
      .timeout(Duration.ofSeconds(5)).uri(uri).build();

  return httpClient
      .sendAsync(request,
          HttpResponse.BodyHandlers.discarding())
      .thenApply(HttpResponse::statusCode)
      .thenApply(statusCode -> statusCode == 200)
      .exceptionally(ex -> false).thenAccept(valid -> {
        if (valid) {
          System.out.printf("[SUCCESS] Verified %s%n", uri);
        } else {
          System.out.printf(
              "[FAILURE] Failed to verify%s%n", uri);
        }
      });
}
```

## Transform Future Result with thenApply

This example shows how to chain transformations using `thenApply`. It generates  
a random number asynchronously and then applies a transformation (adding one)  
to the result. The example also demonstrates proper executor shutdown.

```java

// A random supplier that sleeps for a second, and then returns
// a random value
class RandomSupplier implements Supplier<Integer> {

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
public static class AddOne
    implements Function<Integer, Integer> {

  @Override
  public Integer apply(Integer x) {

    return x + 1;
  }
}

void main() throws Exception {

  ExecutorService exec = Executors
      .newSingleThreadExecutor();

  CompletableFuture<Integer> future = CompletableFuture
      .supplyAsync(new RandomSupplier(), exec);
  IO.println(future.isDone()); // false
  
  CompletableFuture<Integer> f2 = future
      .thenApply(new AddOne());
  IO.println(f2.get()); // Waits until the "calculation" is done and
                                // prints the result

  exec.shutdown();

  try {
    if (!exec.awaitTermination(4, TimeUnit.SECONDS)) {
      exec.shutdownNow();
    }
  } catch (InterruptedException e) {
    exec.shutdownNow();
  }
}
```

## Execute Multiple Tasks in Parallel

This example demonstrates executing multiple tasks concurrently using  
CompletableFuture's default fork-join pool. It measures the execution time to  
show the performance benefits of parallel execution compared to sequential  
processing, completing 10 one-second tasks in approximately one second.

```java

class Task {

  private final int duration;

  public Task(int duration) {
    this.duration = duration;
  }

  public int doTask() {
    System.out.printf("%s %n",
        Thread.currentThread().getName());

    try {
      Thread.sleep(duration * 1000);
    } catch (final InterruptedException e) {
      throw new RuntimeException(e);
    }

    return duration;
  }
}

void main() {

  long start = System.nanoTime();

  List<Task> tasks = IntStream.range(0, 10)
      .mapToObj(i -> new Task(1))
      .collect(Collectors.toList());

  List<CompletableFuture<Integer>> futures = tasks.stream()
      .map(task -> CompletableFuture
          .supplyAsync(task::doTask))
      .collect(Collectors.toList());

  List<Integer> result = futures.stream()
      .map(CompletableFuture::join)
      .collect(Collectors.toList());

  long end = System.nanoTime();

  long duration = (end - start) / 1_000_000;

  System.out.printf("Run %d tasks in %d millis\n",
      tasks.size(), duration);
  System.out.println(result);
}
```

## Simple Async Computation with supplyAsync

This example shows the most basic use of `supplyAsync` to perform a computation  
asynchronously. The task sleeps for 2 seconds and returns a result, while the  
main thread continues execution without blocking.

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;

void main() throws Exception {

  CompletableFuture<String> future = CompletableFuture
      .supplyAsync(() -> {
        try {
          TimeUnit.SECONDS.sleep(2);
        } catch (InterruptedException e) {
          throw new RuntimeException(e);
        }
        return "Hello from async task";
      });

  System.out.println("Doing other work...");
  
  String result = future.get();
  System.out.println(result);
}
```

## Run Task Without Return Value Using runAsync

This example demonstrates `runAsync` for executing tasks that don't return a  
value. It's useful for fire-and-forget operations like logging, notifications,  
or cleanup tasks.

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;

void main() throws Exception {

  CompletableFuture<Void> future = CompletableFuture
      .runAsync(() -> {
        try {
          TimeUnit.SECONDS.sleep(1);
          System.out.println("Task completed in background");
        } catch (InterruptedException e) {
          throw new RuntimeException(e);
        }
      });

  System.out.println("Main thread continues...");
  future.get(); // Wait for completion
  System.out.println("Done");
}
```

## Exception Handling with exceptionally

This example shows how to handle exceptions gracefully using `exceptionally`.  
When an exception occurs in the async task, the exceptionally handler provides  
a fallback value, preventing the entire chain from failing.

```java
import java.util.concurrent.CompletableFuture;

void main() {

  CompletableFuture<Integer> future = CompletableFuture
      .supplyAsync(() -> {
        if (Math.random() > 0.5) {
          throw new RuntimeException("Random failure!");
        }
        return 42;
      })
      .exceptionally(ex -> {
        System.out.println("Error: " + ex.getMessage());
        return -1; // Fallback value
      });

  System.out.println("Result: " + future.join());
}
```

## Handle Both Success and Failure with handle

The `handle` method allows you to process both successful results and  
exceptions in a single callback. Unlike `exceptionally`, it's always called  
regardless of whether the computation succeeded or failed.

```java
import java.util.concurrent.CompletableFuture;

void main() {

  CompletableFuture<String> future = CompletableFuture
      .supplyAsync(() -> {
        if (Math.random() > 0.5) {
          throw new RuntimeException("Failed");
        }
        return "Success";
      })
      .handle((result, ex) -> {
        if (ex != null) {
          return "Recovered from: " + ex.getMessage();
        }
        return result;
      });

  System.out.println(future.join());
}
```

## Perform Actions After Completion with whenComplete

The `whenComplete` method executes a callback when the future completes,  
whether successfully or exceptionally. Unlike `handle`, it doesn't transform  
the result, making it ideal for logging or cleanup operations.

```java
import java.util.concurrent.CompletableFuture;

void main() throws Exception {

  CompletableFuture<String> future = CompletableFuture
      .supplyAsync(() -> {
        return "Task result";
      })
      .whenComplete((result, ex) -> {
        if (ex != null) {
          System.out.println("Failed with: " + ex.getMessage());
        } else {
          System.out.println("Completed with: " + result);
        }
      });

  future.get();
}
```

## Chain Dependent Futures with thenCompose

This example demonstrates `thenCompose` for chaining dependent asynchronous  
operations. It's similar to flatMap in streams, preventing nested  
CompletableFutures and maintaining a flat structure.

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;

void main() {

  CompletableFuture<String> future = CompletableFuture
      .supplyAsync(() -> {
        return "user123";
      })
      .thenCompose(userId -> CompletableFuture.supplyAsync(() -> {
        try {
          TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
          throw new RuntimeException(e);
        }
        return "User details for: " + userId;
      }));

  System.out.println(future.join());
}
```

## Execute Action with thenAccept

The `thenAccept` method consumes the result of a CompletableFuture without  
returning a new value. It's useful for side effects like printing, saving to  
database, or sending notifications.

```java
import java.util.concurrent.CompletableFuture;

void main() throws Exception {

  CompletableFuture<Void> future = CompletableFuture
      .supplyAsync(() -> "Processing data")
      .thenAccept(result -> {
        System.out.println("Received: " + result);
        // Perform side effects here
      });

  future.get();
}
```

## Run Action After Completion with thenRun

The `thenRun` method executes a Runnable after the future completes, ignoring  
the result entirely. It's useful for cleanup, logging, or triggering subsequent  
operations that don't need the result.

```java
import java.util.concurrent.CompletableFuture;

void main() throws Exception {

  CompletableFuture<Void> future = CompletableFuture
      .supplyAsync(() -> "Some result")
      .thenRun(() -> {
        System.out.println("Computation finished, cleaning up...");
      });

  future.get();
}
```

## Wait for All Futures with allOf

This example shows how to wait for multiple independent futures to complete  
using `allOf`. It's essential for coordinating parallel operations and  
collecting results when all tasks are done.

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;
import java.util.Arrays;
import java.util.List;

void main() {

  CompletableFuture<String> future1 = CompletableFuture
      .supplyAsync(() -> {
        sleep(1);
        return "Result 1";
      });

  CompletableFuture<String> future2 = CompletableFuture
      .supplyAsync(() -> {
        sleep(2);
        return "Result 2";
      });

  CompletableFuture<String> future3 = CompletableFuture
      .supplyAsync(() -> {
        sleep(1);
        return "Result 3";
      });

  CompletableFuture<Void> allFutures = CompletableFuture
      .allOf(future1, future2, future3);

  allFutures.join();

  List<String> results = Arrays.asList(
      future1.join(), 
      future2.join(), 
      future3.join()
  );
  
  System.out.println("All results: " + results);
}

void sleep(int seconds) {
  try {
    TimeUnit.SECONDS.sleep(seconds);
  } catch (InterruptedException e) {
    throw new RuntimeException(e);
  }
}
```

## Get First Completed Future with anyOf

The `anyOf` method returns a future that completes when any of the provided  
futures completes. It's useful for implementing race conditions, timeout  
patterns, or getting the fastest response from multiple sources.

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;

void main() {

  CompletableFuture<String> future1 = CompletableFuture
      .supplyAsync(() -> {
        sleep(3);
        return "Slow service";
      });

  CompletableFuture<String> future2 = CompletableFuture
      .supplyAsync(() -> {
        sleep(1);
        return "Fast service";
      });

  CompletableFuture<Object> firstCompleted = CompletableFuture
      .anyOf(future1, future2);

  System.out.println("First result: " + firstCompleted.join());
}

void sleep(int seconds) {
  try {
    TimeUnit.SECONDS.sleep(seconds);
  } catch (InterruptedException e) {
    throw new RuntimeException(e);
  }
}
```

## Use Custom Executor

This example demonstrates using a custom executor with CompletableFuture.  
Custom executors allow fine-grained control over thread pools, enabling  
optimization for specific workloads and resource management.

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;

void main() {

  ExecutorService executor = Executors.newFixedThreadPool(3);

  CompletableFuture<String> future = CompletableFuture
      .supplyAsync(() -> {
        System.out.println("Running in: " + 
            Thread.currentThread().getName());
        return "Result from custom executor";
      }, executor);

  System.out.println(future.join());

  executor.shutdown();
  try {
    if (!executor.awaitTermination(5, TimeUnit.SECONDS)) {
      executor.shutdownNow();
    }
  } catch (InterruptedException e) {
    executor.shutdownNow();
  }
}
```

## Combine Two Independent Futures

This example shows combining two independent futures using `thenCombine`. Both  
futures execute in parallel, and their results are combined using a  
BiFunction when both complete.

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;

void main() {

  CompletableFuture<Integer> future1 = CompletableFuture
      .supplyAsync(() -> {
        sleep(1);
        return 10;
      });

  CompletableFuture<Integer> future2 = CompletableFuture
      .supplyAsync(() -> {
        sleep(1);
        return 20;
      });

  CompletableFuture<Integer> combined = future1
      .thenCombine(future2, (result1, result2) -> {
        return result1 + result2;
      });

  System.out.println("Sum: " + combined.join());
}

void sleep(int seconds) {
  try {
    TimeUnit.SECONDS.sleep(seconds);
  } catch (InterruptedException e) {
    throw new RuntimeException(e);
  }
}
```

## Async Variants: thenApplyAsync vs thenApply

This example compares synchronous and asynchronous transformation methods.  
Methods ending with "Async" execute in a different thread from the ForkJoinPool,  
while non-async variants may run in the completing thread.

```java
import java.util.concurrent.CompletableFuture;

void main() throws Exception {

  // thenApply - may run in the same thread
  CompletableFuture<String> future1 = CompletableFuture
      .supplyAsync(() -> {
        System.out.println("Supply: " + Thread.currentThread().getName());
        return "Hello";
      })
      .thenApply(s -> {
        System.out.println("Apply: " + Thread.currentThread().getName());
        return s + " World";
      });

  // thenApplyAsync - runs in a different thread
  CompletableFuture<String> future2 = CompletableFuture
      .supplyAsync(() -> {
        System.out.println("Supply Async: " + Thread.currentThread().getName());
        return "Hello";
      })
      .thenApplyAsync(s -> {
        System.out.println("Apply Async: " + Thread.currentThread().getName());
        return s + " World";
      });

  System.out.println(future1.get());
  System.out.println(future2.get());
}
```

## Create Already Completed Future

The `completedFuture` method creates a CompletableFuture that is already  
completed with a given value. It's useful for testing, providing default  
values, or when you need to return a Future but have the value immediately.

```java
import java.util.concurrent.CompletableFuture;

void main() {

  CompletableFuture<String> immediate = CompletableFuture
      .completedFuture("Already done");

  System.out.println("Is done: " + immediate.isDone());
  System.out.println("Result: " + immediate.join());
}
```

## Combine Actions with thenAcceptBoth

This method executes an action when two futures complete, consuming both  
results. Unlike `thenCombine`, it doesn't return a value, making it suitable  
for side effects that depend on two asynchronous results.

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;

void main() throws Exception {

  CompletableFuture<String> future1 = CompletableFuture
      .supplyAsync(() -> {
        sleep(1);
        return "First";
      });

  CompletableFuture<String> future2 = CompletableFuture
      .supplyAsync(() -> {
        sleep(1);
        return "Second";
      });

  CompletableFuture<Void> combined = future1
      .thenAcceptBoth(future2, (result1, result2) -> {
        System.out.println("Combined: " + result1 + " and " + result2);
      });

  combined.get();
}

void sleep(int seconds) {
  try {
    TimeUnit.SECONDS.sleep(seconds);
  } catch (InterruptedException e) {
    throw new RuntimeException(e);
  }
}
```

## Run After Both Futures Complete

The `runAfterBoth` method executes a Runnable after two futures complete,  
ignoring both results. It's useful for synchronization points in complex  
asynchronous workflows.

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;

void main() throws Exception {

  CompletableFuture<Void> future1 = CompletableFuture
      .runAsync(() -> {
        sleep(1);
        System.out.println("Task 1 done");
      });

  CompletableFuture<Void> future2 = CompletableFuture
      .runAsync(() -> {
        sleep(2);
        System.out.println("Task 2 done");
      });

  CompletableFuture<Void> both = future1
      .runAfterBoth(future2, () -> {
        System.out.println("Both tasks completed!");
      });

  both.get();
}

void sleep(int seconds) {
  try {
    TimeUnit.SECONDS.sleep(seconds);
  } catch (InterruptedException e) {
    throw new RuntimeException(e);
  }
}
```

## Accept First Completed Result

The `acceptEither` method processes the result of whichever future completes  
first. It's useful when you have multiple sources and want to act on the  
fastest response.

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;

void main() throws Exception {

  CompletableFuture<String> slow = CompletableFuture
      .supplyAsync(() -> {
        sleep(3);
        return "Slow result";
      });

  CompletableFuture<String> fast = CompletableFuture
      .supplyAsync(() -> {
        sleep(1);
        return "Fast result";
      });

  CompletableFuture<Void> either = fast
      .acceptEither(slow, result -> {
        System.out.println("First to complete: " + result);
      });

  either.get();
}

void sleep(int seconds) {
  try {
    TimeUnit.SECONDS.sleep(seconds);
  } catch (InterruptedException e) {
    throw new RuntimeException(e);
  }
}
```

## Apply Function to First Completed Future

The `applyToEither` method applies a function to whichever future completes  
first, returning a new CompletableFuture with the transformed result. It's  
ideal for implementing fallback mechanisms or redundant service calls.

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;

void main() {

  CompletableFuture<Integer> service1 = CompletableFuture
      .supplyAsync(() -> {
        sleep(2);
        return 100;
      });

  CompletableFuture<Integer> service2 = CompletableFuture
      .supplyAsync(() -> {
        sleep(1);
        return 200;
      });

  CompletableFuture<Integer> fastest = service1
      .applyToEither(service2, result -> result * 2);

  System.out.println("Fastest doubled: " + fastest.join());
}

void sleep(int seconds) {
  try {
    TimeUnit.SECONDS.sleep(seconds);
  } catch (InterruptedException e) {
    throw new RuntimeException(e);
  }
}
```

## Complete Future Manually

This example shows how to manually complete a CompletableFuture using  
`complete()` or `completeExceptionally()`. This is useful for integrating with  
callback-based APIs or implementing custom async operations.

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;

void main() throws Exception {

  CompletableFuture<String> future = new CompletableFuture<>();

  // Simulate async callback
  new Thread(() -> {
    try {
      TimeUnit.SECONDS.sleep(2);
      future.complete("Manually completed");
    } catch (Exception e) {
      future.completeExceptionally(e);
    }
  }).start();

  System.out.println("Waiting for result...");
  System.out.println("Result: " + future.get());
}
```

## Timeout Handling with orTimeout

The `orTimeout` method (Java 9+) completes the future exceptionally if it  
doesn't complete within the specified timeout. It's essential for preventing  
indefinite waits on slow or hanging operations.

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;

void main() {

  CompletableFuture<String> future = CompletableFuture
      .supplyAsync(() -> {
        sleep(5);
        return "This takes too long";
      })
      .orTimeout(2, TimeUnit.SECONDS)
      .exceptionally(ex -> {
        return "Timed out!";
      });

  System.out.println(future.join());
}

void sleep(int seconds) {
  try {
    TimeUnit.SECONDS.sleep(seconds);
  } catch (InterruptedException e) {
    throw new RuntimeException(e);
  }
}
```

## Provide Default Value on Timeout

The `completeOnTimeout` method (Java 9+) completes the future with a default  
value if it doesn't complete within the timeout. Unlike `orTimeout`, it doesn't  
throw an exception, providing a graceful fallback.

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;

void main() {

  CompletableFuture<String> future = CompletableFuture
      .supplyAsync(() -> {
        sleep(5);
        return "Slow result";
      })
      .completeOnTimeout("Default value", 2, TimeUnit.SECONDS);

  System.out.println(future.join());
}

void sleep(int seconds) {
  try {
    TimeUnit.SECONDS.sleep(seconds);
  } catch (InterruptedException e) {
    throw new RuntimeException(e);
  }
}
```

## Fetch Data from Multiple APIs in Parallel

This practical example demonstrates fetching data from multiple APIs  
concurrently and combining the results. It shows a real-world pattern for  
improving application performance through parallel data retrieval.

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;
import java.util.List;
import java.util.stream.Collectors;

void main() {

  List<String> userIds = List.of("user1", "user2", "user3", "user4", "user5");

  long start = System.currentTimeMillis();

  List<CompletableFuture<String>> futures = userIds.stream()
      .map(userId -> CompletableFuture.supplyAsync(() -> {
        return fetchUserData(userId);
      }))
      .collect(Collectors.toList());

  CompletableFuture<Void> allFutures = CompletableFuture
      .allOf(futures.toArray(new CompletableFuture[0]));

  CompletableFuture<List<String>> allResults = allFutures
      .thenApply(_ -> futures.stream()
          .map(CompletableFuture::join)
          .collect(Collectors.toList()));

  List<String> results = allResults.join();
  long end = System.currentTimeMillis();

  System.out.println("Results: " + results);
  System.out.println("Time taken: " + (end - start) + "ms");
}

String fetchUserData(String userId) {
  try {
    TimeUnit.MILLISECONDS.sleep(500); // Simulate API call
  } catch (InterruptedException e) {
    throw new RuntimeException(e);
  }
  return "Data for " + userId;
}
```

