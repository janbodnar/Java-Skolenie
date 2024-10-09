# HttpClient


## HTTP

The Hypertext Transfer Protocol (HTTP) is an application protocol for  
distributed, collaborative, hypermedia information systems. HTTP is the  
foundation of data communication for the World Wide Web.  

In the examples, we use httpbin.org, which is a freely available HTTP request  
and response service, and the webcode.me, which is a tiny HTML page for testing.  

## HttpClient

Java 11 introduced HttpClient library. Before Java 11, developers had to use  
rudimentary URLConnection, or use third-party library such as Apache HttpClient,  
or OkHttp.  

The Java HTTP Client supports both HTTP/1.1 and HTTP/2. By default the client  
will send requests using HTTP/2. Requests sent to servers that do not yet  
support HTTP/2 will automatically be downgraded to HTTP/1.1.  

```java
client = HttpClient.newHttpClient();
client = HttpClient.newBuilder().build();
```

There are two ways to create an `HttpClient`. The code creates new client with
default settings.

## Status

In the first example, we determine the status of a web page.

```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

void main() throws IOException, InterruptedException {

    try (HttpClient client = HttpClient.newHttpClient()) {
        
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://webcode.me"))
                .GET() // GET is default
                .build();

        HttpResponse<Void> response = client.send(request,
                HttpResponse.BodyHandlers.discarding());

        System.out.println(response.statusCode());
    }
}
```

The example creates a GET request to the `webcode.me` website and retrives an  
http response. From the response, we get the status code.  

```java
HttpClient client = HttpClient.newHttpClient();
```

A new `HttpClient` is created.

```java
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://webcode.me"))
    .GET() // GET is default
    .build();
```

A new `HttpRequest` is built. We specify the `URI` and the request method.  
(If we do not specify the request method, the default is GET.)

```java
HttpResponse<Void> response = client.send(request,
    HttpResponse.BodyHandlers.discarding());
```

We send the request. Since we are not interested in the response body, we  
discard it with the HttpResponse.BodyHandlers.discarding.  

```java
System.out.println(response.statusCode());
```

We get the status code with the statusCode method.

## HEAD request

A HEAD request is a GET request without a message body.

```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpHeaders;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

void main() throws IOException, InterruptedException {

    try (HttpClient client = HttpClient.newHttpClient()) {

        var request = HttpRequest.newBuilder(URI.create("https://webcode.me"))
                .method("HEAD", HttpRequest.BodyPublishers.noBody())
                .build();

        HttpResponse<Void> response = client.send(request,
                HttpResponse.BodyHandlers.discarding());

        HttpHeaders headers = response.headers();

        headers.map().forEach((key, values) -> {
            System.out.printf("%s: %s%n", key, values);
        });
    }
}
```

The example creates a HEAD request.

```java
var request = HttpRequest.newBuilder(URI.create("https://webcode.me"))
    .method("HEAD", HttpRequest.BodyPublishers.noBody())
    .build();
```

We build a `HEAD` request. We use `HttpRequest.BodyPublishers.noBody` since we  
do not have any body in the request.

```java
HttpResponse<Void> response = client.send(request,
    HttpResponse.BodyHandlers.discarding());
```

We send a request and receive a body.

```java
HttpHeaders headers = response.headers();

headers.map().forEach((key, values) -> {
    System.out.printf("%s: %s%n", key, values);
});
```

We get the headers from the response and print them to the console.


## GET request

The HTTP GET method requests a representation of the specified resource.  
Requests using GET should only retrieve data.  

```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

void main() throws IOException, InterruptedException {

    try (HttpClient client = HttpClient.newHttpClient()) {

        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://webcode.me"))
                .build();

        HttpResponse<String> response = client.send(request,
                HttpResponse.BodyHandlers.ofString());

        System.out.println(response.body());
    }
}
```

We create a GET request to the webcode.me webpage.

```java
try (HttpClient client = HttpClient.newHttpClient()) {
```

A new `HttpClient` is created with the `newHttpClient` factory method.

```java
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://webcode.me"))
    .build();
```

We build a synchronous request to the webpage. The default method is GET.

```java
HttpResponse<String> response = client.send(request,
    HttpResponse.BodyHandlers.ofString());

System.out.println(response.body());
```

We send the request and retrieve the content of the response and print it to the  
console. We use `HttpResponse.BodyHandlers.ofString` since we expect a string  
HTML response.  


## File bodyhandler

With file bodyhandler we can easily write the response text to a file.  

```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.nio.file.Path;
import java.nio.file.Paths;

void main() throws IOException, InterruptedException {

    try (HttpClient client = HttpClient.newHttpClient()) {

        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://webcode.me"))
                .GET() // GET is default
                .build();

        String fileName = "src/main/resources/index.html";

        HttpResponse<Path> response = client.send(request,
                HttpResponse.BodyHandlers.ofFile(Paths.get(fileName)));

        System.out.println(response.statusCode());
    }
}
```

The example writes the HTML page to `src/main/resources/index.html` file.  

```java
String fileName = "src/main/resources/index.html";

HttpResponse<Path> response = client.send(request,
        HttpResponse.BodyHandlers.ofFile(Paths.get(fileName)));
```

The file bodyhandler is created with `HttpResponse.BodyHandlers.ofFile`.

## POST request

The HTTP POST method sends data to the server. It is often used when uploading a  
file or when submitting a completed web form.  

```xml
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.11.0</version>
</dependency>
```

We need the `gson` dependency.

```java
import com.google.gson.Gson;

import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.util.HashMap;

void main() throws IOException, InterruptedException {

    var values = new HashMap<String, String>() {{
        put("name", "John Doe");
        put("occupation", "gardener");
    }};

    Gson gson = new Gson();
    String requestBody = gson.toJson(values);

    try (HttpClient client = HttpClient.newHttpClient()) {

        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://httpbin.org/post"))
                .POST(HttpRequest.BodyPublishers.ofString(requestBody))
                .build();

        HttpResponse<String> response = client.send(request,
                HttpResponse.BodyHandlers.ofString());

        System.out.println(response.body());
    }
}
```

We send a POST request to the `https://httpbin.org/post` page.

```java
var values = new HashMap<String, String>() {{
    put("name", "John Doe");
    put ("occupation", "gardener");
}};

Gson gson = new Gson();
String requestBody = gson.toJson(values);
```

We build the request body with the Gson.

```java
try (HttpClient client = HttpClient.newHttpClient()) {
    
    HttpRequest request = HttpRequest.newBuilder()
            .uri(URI.create("https://httpbin.org/post"))
            .POST(HttpRequest.BodyPublishers.ofString(requestBody))
            .build();
    ...
}
```

We build the POST request. With `BodyPublishers.ofString` we create a new  
BodyPublisher. It converts high-level Java objects into a flow of byte buffers  
suitable for sending as a request body.  

```java
HttpResponse<String> response = client.send(request,
        HttpResponse.BodyHandlers.ofString());

System.out.println(response.body());
```

We send the request and retrieve the response.

## Redirect

Redirection is a process of forwarding one URL to a different URL. The HTTP  
response status code 301 Moved Permanently is used for permanent URL  
redirection; 302 Found for a temporary redirection.  

```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

// toggle HttpClient.Redirect.ALWAYS / HttpClient.Redirect.NEVER

void main() throws IOException, InterruptedException {

    try (HttpClient client = HttpClient.newBuilder()
            .followRedirects(HttpClient.Redirect.ALWAYS).build()) {

        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://httpbin.org/redirect/3"))
                .GET()
                .build();

        HttpResponse<Void> response = client.send(request,
                HttpResponse.BodyHandlers.discarding());

        System.out.println(response.statusCode());
    }
}
```

In the example, we send a request that is redirected.

```java
try (HttpClient client = HttpClient.newBuilder()
        .followRedirects(HttpClient.Redirect.ALWAYS).build()) {
    ...
}
```

To configure redirection, we use the `followRedirects` method.

```java
HttpRequest request = HttpRequest.newBuilder()
        .uri(URI.create("https://httpbin.org/redirect/3"))
        .GET()
        .build();
```

The `https://httpbin.org/redirect/3` is a test URL that redirects the request  
three times.

```java
HttpResponse<Void> response = client.send(request,
        HttpResponse.BodyHandlers.discarding());

System.out.println(response.statusCode());
```

The request is sent and the response status is printed.

## Read favicon

The following example reads a small image from a website.

```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

void main() throws IOException, InterruptedException {

    try (HttpClient client = HttpClient.newHttpClient()) {

        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://webcode.me/favicon.ico"))
                .build();

        HttpResponse<byte[]> response = client.send(request,
                HttpResponse.BodyHandlers.ofByteArray());

        byte[] data = response.body();

        int i = 0;

        for (byte c : data) {

            System.out.printf("%02x ", c);

            i++;

            if (i % 10 == 0) {

                System.out.println();
            }
        }
    }
}
```

The example reads a favicon from a website and prints its contents in  
hexadecimal format.

```java
HttpResponse<byte[]> response = client.send(request,
    HttpResponse.BodyHandlers.ofByteArray());
```

With `HttpResponse.BodyHandlers.ofByteArray` we read binary data.  

```java
byte[] data = response.body();
```

We get the array of bytes from the response body.

```java
int i = 0;
for (byte c : data) {

    System.out.printf("%02x ", c);

    i++;

    if (i % 10 == 0) {

        System.out.println();
    }
}
```

In a for loop, we output the bytes in hexadecimal format.
