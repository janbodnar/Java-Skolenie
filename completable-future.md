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
