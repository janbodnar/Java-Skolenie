# Jdbi

Jdbi provides convenient, idiomatic, access to relational data in Java. Jdbi 3  
is the third major release, which introduces enhanced support for modern Java,  
countless refinements to the design and implementation, and enhanced support for  
modular development through plugins and extensions.  
  
Jdbi is built on top of JDBC. If your data source has a JDBC driver, you can use  
it with Jdbi. It improves JDBC’s low-level interface, providing a more natural  
API that is easy to bind to your domain data types.  

Jdbi is a solution between JDBC and ORM.

```xml
<dependency>
    <groupId>org.jdbi</groupId>
    <artifactId>jdbi3-core</artifactId>
    <version>3.45.2</version>
</dependency>

<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.7.3</version>
</dependency>

<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <version>2.2.224</version>
</dependency>
```

For the examples, we need an `jdbi3-core` artifact and a database driver such  
as `h2` or `postgresql`.


## Simple query

```java
import org.jdbi.v3.core.Jdbi;

void main() {

    String jdbcUrl = "jdbc:h2:mem:";

    Jdbi jdbi = Jdbi.create(jdbcUrl);

    int res = jdbi.withHandle(handle -> handle.createQuery("SELECT 2 + 2")
            .mapTo(Integer.class)
            .one());

    System.out.println(res);
}
```

## Calling function

The `H2VERSION` function returns the version of the H2 database.  

```java
import org.jdbi.v3.core.Jdbi;

void main() {

    String jdbcUrl = "jdbc:h2:mem:";

    Jdbi jdbi = Jdbi.create(jdbcUrl);

    String res = jdbi.withHandle(handle -> handle.createQuery("SELECT H2VERSION()")
            .mapTo(String.class)
            .one());

    System.out.println(res);
}
```

## PostgreSQL version 

To get the version of PostgreSQL database, we call the `VERSION` function.  

```java
import org.jdbi.v3.core.Jdbi;

void main() {

    String jdbcUrl = "jdbc:postgresql://localhost:5432/testdb";
    String user = "postgres";
    String password = "s$cret";

    Jdbi jdbi = Jdbi.create(jdbcUrl, user, password);

    String res = jdbi.withHandle(handle -> handle.createQuery("SELECT VERSION()")
            .mapTo(String.class)
            .one());

    System.out.println(res);
}
```

## Batches 

A *batch* refers to a group of SQL statements that are submitted and executed  
together as a single unit. This functionality offers performance benefits and  
simplifies code for certain database operations.  

```java
import org.jdbi.v3.core.Jdbi;

void main() {

    String jdbcUrl = "jdbc:postgresql://localhost:5432/testdb";
    String user = "postgres";
    String password = "andrea";

    Jdbi jdbi = Jdbi.create(jdbcUrl, user, password);

    jdbi.withHandle(handle -> handle.createBatch()
            .add("DROP TABLE IF EXISTS cars")
            .add("CREATE TABLE cars(id serial PRIMARY KEY, name VARCHAR(255), price INT)")
            .add("INSERT INTO cars(name, price) VALUES('Audi',52642)")
            .add("INSERT INTO cars(name, price) VALUES('Mercedes',57127)")
            .add("INSERT INTO cars(name, price) VALUES('Skoda',9000)")
            .add("INSERT INTO cars(name, price) VALUES('Volvo',29000)")
            .add("INSERT INTO cars(name, price) VALUES('Bentley',350000)")
            .add("INSERT INTO cars(name, price) VALUES('Citroen',21000)")
            .add("INSERT INTO cars(name, price) VALUES('Hummer',41400)")
            .add("INSERT INTO cars(name, price) VALUES('Volkswagen',21600)")

            .execute());

    System.out.println("Table created and data inserted using JDBI batch.");
}
```

## Queries

Queries are executed with `select`.  

The `one` method returns when you expect the result to contain exactly one row.  
This method returns `null` only if the returned row maps to `null` and throws an  
exception if the result has zero or multiple rows.  


```java
import org.jdbi.v3.core.Jdbi;

void main() {

    String jdbcUrl = "jdbc:postgresql://localhost:5432/testdb";
    String user = "postgres";
    String password = "s$cret";

    Jdbi jdbi = Jdbi.create(jdbcUrl, user, password);

    String res = jdbi.withHandle(handle -> handle.select("SELECT name FROM cars WHERE id = ?", 3)
                    .mapTo(String.class)
                    .one());


    System.out.println(res);
}
```

The `findOne` method returns an `Optional`.  

```java
import org.jdbi.v3.core.Jdbi;

import java.util.Optional;

void main() {

    String jdbcUrl = "jdbc:postgresql://localhost:5432/testdb";
    String user = "postgres";
    String password = "s$cret";

    Jdbi jdbi = Jdbi.create(jdbcUrl, user, password);

    int id = 3;

    Optional<String> res = jdbi.withHandle(handle -> handle.select("SELECT name FROM cars WHERE id = ?", id)
            .mapTo(String.class)
            .findOne());

    res.ifPresentOrElse(System.out::println, () -> System.out.println("N/A"));
}
```

## Mapping a row to a class/record

```java
import java.util.Optional;
import org.jdbi.v3.core.Jdbi;
import org.jdbi.v3.core.mapper.reflect.ConstructorMapper;

void main() {

    String jdbcUrl = "jdbc:postgresql://localhost:5432/testdb";
    String user = "postgres";
    String password = "s$cret";

    Jdbi jdbi = Jdbi.create(jdbcUrl, user, password);

    int id = 3;

    Optional<Car> res = jdbi.withHandle(handle -> handle.select("SELECT * FROM cars WHERE id = ?", id)
            .registerRowMapper(Car.class, ConstructorMapper.of(Car.class))
            .mapTo(Car.class)
            .findOne());

    res.ifPresentOrElse(System.out::println, () -> System.out.println("N/A"));
}

public record Car(int id, String name, int price) {
}
```

## Binding of parameters 

Parameter binding is a mechanism to prevent SQL injection vulnerabilities and  
improve code readability. You can bind values to placeholders within your SQL  
statements, and JDBI handles setting the actual values for the database  
execution.  

Types of binding:  

- positional
- positional
- named
- bean binding 


Positional binding example:  

```java
import org.jdbi.v3.core.Jdbi;
import org.jdbi.v3.core.mapper.reflect.ConstructorMapper;

import java.util.Optional;

void main() {

    String jdbcUrl = "jdbc:postgresql://localhost:5432/testdb";
    String user = "postgres";
    String password = "s$cret";

    Jdbi jdbi = Jdbi.create(jdbcUrl, user, password);

    int id = 3;

    Optional<Car> res = jdbi.withHandle(handle -> handle.select("SELECT * FROM cars WHERE id = ?", id)
            .registerRowMapper(Car.class, ConstructorMapper.of(Car.class))
            .mapTo(Car.class)
            .findOne());

    res.ifPresentOrElse(System.out::println, () -> System.out.println("N/A"));
}

public record Car(int id, String name, int price) {
}
```


Named binding example:  

```java
import org.jdbi.v3.core.Jdbi;
import org.jdbi.v3.core.mapper.reflect.ConstructorMapper;

import java.util.Optional;

void main() {

    String jdbcUrl = "jdbc:postgresql://localhost:5432/testdb";
    String user = "postgres";
    String password = "s$cret";

    Jdbi jdbi = Jdbi.create(jdbcUrl, user, password);

    int id = 3;

    Optional<Car> res = jdbi.withHandle(handle -> handle.select("SELECT * FROM cars WHERE id = :id")
            .registerRowMapper(Car.class, ConstructorMapper.of(Car.class))
            .bind("id", id)
            .mapTo(Car.class)
            .findOne());

    res.ifPresentOrElse(System.out::println, () -> System.out.println("N/A"));
}

public record Car(int id, String name, int price) {
}
```


## Mapping rows to a list 

```java
import org.jdbi.v3.core.Jdbi;
import org.jdbi.v3.core.mapper.reflect.ConstructorMapper;

import java.util.List;

void main() {

    String jdbcUrl = "jdbc:postgresql://localhost:5432/testdb";
    String user = "postgres";
    String password = "s$cret";

    Jdbi jdbi = Jdbi.create(jdbcUrl, user, password);

    List<Car> cars = jdbi.withHandle(handle -> handle.select("SELECT * FROM cars")
            .registerRowMapper(Car.class, ConstructorMapper.of(Car.class))
            .mapTo(Car.class)
            .list());

    if (cars.isEmpty()) {

        System.out.println("No cars found.");
    } else {
        
        System.out.println("List of cars:");
        cars.forEach(System.out::println);
    }
}

public record Car(int id, String name, int price) {
}
```

## SqlObjects

Jdbi SqlObjects is an extension for the Jdbi library that provides a declarative  
way to interact with relational databases in Java.  

We need to add the `jdbi3-sqlobject` dependency.  

```xml
<dependency>
    <groupId>org.jdbi</groupId>
    <artifactId>jdbi3-sqlobject</artifactId>
    <version>3.45.2</version>
</dependency>
```


```java
import org.jdbi.v3.core.Jdbi;
import org.jdbi.v3.core.mapper.reflect.ConstructorMapper;
import org.jdbi.v3.sqlobject.SqlObject;
import org.jdbi.v3.sqlobject.SqlObjectPlugin;
import org.jdbi.v3.sqlobject.statement.SqlQuery;

import java.util.Optional;

void main() {

    String jdbcUrl = "jdbc:postgresql://localhost:5432/testdb";
    String user = "postgres";
    String password = "s$cret";

    Jdbi jdbi = Jdbi.create(jdbcUrl, user, password);
    jdbi.installPlugin(new SqlObjectPlugin());

    jdbi.registerRowMapper(Car.class, ConstructorMapper.of(Car.class));
    CarDao carDao = jdbi.onDemand(CarDao.class);

    int searchId = 2;
    Optional<Car> car = carDao.findById(searchId);

    if (car.isPresent()) {
        System.out.println("Car found: " + car.get());
    } else {
        System.out.println("Car with id " + searchId + " not found.");
    }

}

public record Car(int id, String name, int price) {
}

public interface CarDao extends SqlObject {

    @SqlQuery("SELECT * FROM cars WHERE id = ?")
    Optional<Car> findById(int id);
}
```
