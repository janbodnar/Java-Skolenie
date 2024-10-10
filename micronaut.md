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

## DB Example

Dependencies: `micronaut-data-jdbc`, `postgresql`, `snakeyaml`, 

`application.yaml`: 

```yaml
micronaut:
  application:
    name: demo2
datasources:
  default:
    url: jdbc:postgresql://localhost:5432/testdb
    driver-class-name: org.postgresql.Driver
    db-type: postgres
    username: postgres
    password: andrea
```

`User.java`:  

```java
package com.example.model;

import io.micronaut.data.annotation.GeneratedValue;
import io.micronaut.data.annotation.Id;
import io.micronaut.data.annotation.MappedEntity;
import io.micronaut.data.annotation.MappedProperty;
import io.micronaut.serde.annotation.Serdeable;

@Serdeable
@MappedEntity(value = "users")
public class User {


    @Id
    @GeneratedValue(GeneratedValue.Type.AUTO)
    private Long id;

    @MappedProperty("first_name")
    private String firstName;

    @MappedProperty("last_name")
    private String lastName;
    private String occupation;
    private String dob;

    public User() {

    }

    public User(String firstName, String lastName, String occupation, String dob) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.occupation = occupation;
        this.dob = dob;
    }

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    public String getOccupation() {
        return occupation;
    }

    public void setOccupation(String occupation) {
        this.occupation = occupation;
    }

    public String getDob() {
        return dob;
    }

    public void setDob(String dob) {
        this.dob = dob;
    }
}
```

`UserRepository.java`:  

```java
package com.example.repository;

import com.example.model.User;
import io.micronaut.data.jdbc.annotation.JdbcRepository;
import io.micronaut.data.model.query.builder.sql.Dialect;
import io.micronaut.data.repository.CrudRepository;

@JdbcRepository(dialect = Dialect.POSTGRES)
public interface UserRepository extends CrudRepository<User, Long> {
}
```

`MyController.java`: 

```java
package com.example.controller;

import com.example.model.User;
import com.example.repository.UserRepository;
import io.micronaut.http.HttpResponse;
import io.micronaut.http.annotation.Controller;
import io.micronaut.http.annotation.Get;

import java.util.List;

@Controller
public class MyController {

    private final UserRepository userRepository;

    public MyController(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    @Get("/users")
    public List<User> users() {
        return userRepository.findAll();
    }

    @Get("/users/{id}")
    public HttpResponse<User> getUser(Long id) {
        return userRepository.findById(id)
                .map(HttpResponse::ok)
                .orElse(HttpResponse.notFound());
    }
}
```
