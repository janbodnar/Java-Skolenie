# Micronaut

Micronaut is an open-source, JVM-based framework designed for building lightweight, modular  
applications and microservices. It emphasizes fast startup times and low memory consumption,  
making it particularly suitable for cloud-native and serverless environments. 

Unlike traditional frameworks that rely on runtime reflection, Micronaut performs much of its  
work at compile time, which enhances performance and reduces overhead. It supports Java, Groovy,  
and Kotlin, and provides features such as dependency injection, aspect-oriented programming,  
service discovery, and HTTP routing, all while maintaining a minimal footprint and facilitating  
easy testing.

```java
package com.example.controller;

import io.micronaut.http.HttpResponse;
import io.micronaut.http.MediaType;
import io.micronaut.http.annotation.Controller;
import io.micronaut.http.annotation.Get;
import io.micronaut.http.annotation.Produces;
import io.micronaut.views.View;

import java.util.List;
import java.util.Map;

@Controller
public class HelloController {

    @Get("/hello")
    @Produces(MediaType.TEXT_PLAIN)
    public String hello() {

        return "hello there!";
    }

    @Get("/notfound")
    @Produces(MediaType.TEXT_PLAIN)
    public HttpResponse<?> notfound() {

        return HttpResponse.notFound();
    }
    @Get("/status")
    @Produces(MediaType.TEXT_PLAIN)
    public HttpResponse<?> status() {

        return HttpResponse.ok();
    }

    @Get("/words")
    @Produces(MediaType.APPLICATION_JSON)
    public List<String> words() {

        return List.of("sky", "look", "rest", "parrot");
    }

    @View("users")
    @Get("/users")
    HttpResponse<?> index() {
        Map<String, List<User>> users = Map.of("users", List.of(new User("John Doe", "gardener"),
                new User("Roger Roe", "driver")));

        return HttpResponse.ok(users);
    }
}

record User(String name, String occupation) {}
```

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Users</title>
</head>
<body>

<table>
    <thead>
    <tr>
        <th>name</th>
        <th>occupation</th>
    </tr>
    </thead>
    <tbody>
    {% for u in users %}
    <tr>
        <td>{{u.name}}</td>
        <td>{{u.occupation}}</td>
    </tr>
    {% endfor %}

    </tbody>

</table>

</body>
</html>
```

```java
package com.example;

import io.micronaut.core.annotation.Blocking;
import io.micronaut.http.HttpRequest;
import io.micronaut.http.HttpResponse;
import io.micronaut.http.HttpStatus;
import io.micronaut.http.MediaType;
import io.micronaut.http.client.BlockingHttpClient;
import io.micronaut.http.client.HttpClient;
import io.micronaut.http.client.annotation.Client;
import io.micronaut.http.client.exceptions.HttpClientResponseException;
import io.micronaut.runtime.EmbeddedApplication;
import io.micronaut.test.extensions.junit5.annotation.MicronautTest;
import jakarta.inject.Inject;
import org.junit.jupiter.api.Assertions;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertNotNull;
import static org.junit.jupiter.api.Assertions.assertThrows;
import static org.junit.jupiter.api.Assertions.assertThrowsExactly;

@MicronautTest
class DemoTest {

    @Inject
    EmbeddedApplication<?> application;

//    @Inject
//    @Client("/")
//    HttpClient client;

    @Inject
    @Client("/")
    HttpClient client;

    @Test
    @DisplayName(value="Test it works")
    void testItWorks() {
        Assertions.assertTrue(application.isRunning());
    }

    @Test
    @DisplayName(value="Test hello message")
    public void testHello() {
        HttpRequest<?> request = HttpRequest.GET("/hello").accept(MediaType.TEXT_PLAIN);
        String body = client.toBlocking().retrieve(request);

        assertNotNull(body);
        assertEquals("hello there!", body);
    }

    @Test
    @DisplayName("Resource not found")
    void testResourceNotFound() {

        assertThrowsExactly(HttpClientResponseException.class,
                () -> client.retrieve(HttpRequest.GET("/notfound")),
                HttpStatus.NOT_FOUND.getReason());

    }

    @Test
    @DisplayName("Status is OK")
    void testStatusIsOk() {

        HttpResponse<String> response = client.toBlocking().exchange("/status", String.class);
        assertEquals(HttpStatus.OK, response.status());
    }
}
```

