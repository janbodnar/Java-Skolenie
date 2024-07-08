# Jdbi

Jdbi provides convenient, idiomatic, access to relational data in Java. Jdbi 3 is  
the third major release, which introduces enhanced support for modern Java, countless  
refinements to the design and implementation, and enhanced support for modular  
development through plugins and extensions.

Jdbi is built on top of JDBC. If your data source has a JDBC driver, you can use it with  
Jdbi. It improves JDBC’s low-level interface, providing a more natural API that is easy to  
bind to your domain data types.

## Simple query

```java
import org.jdbi.v3.core.Jdbi;

void main() {

    String jdbcUrl = "jdbc:h2:mem:testdb";

    Jdbi jdbi = Jdbi.create(jdbcUrl);

    int res = jdbi.withHandle(handle -> handle.createQuery("SELECT 2 + 2")
            .mapTo(Integer.class)
            .one());

    System.out.println(res);  
}
```
