# SQLite 

SQLite is a **serverless**, **self-contained**, and **embedded** database engine. It's a library  
integrated within applications, allowing them to interact directly with database files. SQLite supports  
**ACID-compliant transactions** and uses **dynamic types** for tables. It's widely used in various systems,  
including web browsers, operating systems, and mobile phones.  

```
java --enable-preview --source 22 -cp lib\sqlite-jdbc-3.46.0.1-20240611.065717-6.jar;lib\slf4j-api-1.7.36.jar Main.java
```

Driver: https://github.com/xerial/sqlite-jdbc  


## Select version 

```java

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.logging.Level;
import java.util.logging.Logger;

void main() {

    String query = "SELECT SQLITE_VERSION()";

    try (Connection con = DriverManager.getConnection("jdbc:sqlite:test.db");
            Statement st = con.createStatement();
            ResultSet rs = st.executeQuery(query)) {

        if (rs.next()) {

            System.out.println(rs.getString(1));
        }

    } catch (SQLException ex) {

        Logger lgr = Logger.getLogger(getClass().getName());
        lgr.log(Level.SEVERE, ex.getMessage(), ex);
    }
}
```

## Create table

When we need to update data with multiple statements, we can use batch updates. Batch updates are available   
for `INSERT`, `UPDATE`, `DELETE`, statements as well as for `CREATE TABLE` and `DROP TABLE` statements.  

Batch processing groups multiple queries into one unit and passes it in a single network trip to a database.  

JDBC does not start a transaction by default when you use `addBatch`. The `addBatch` method simply adds SQL  
statements to the batch, but it doesn’t start a transaction.  

The transaction begins when you set autoCommit to false. If autoCommit is `true` (which is the default setting),  
then each SQL statement is executed as an individual transaction.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.logging.Level;
import java.util.logging.Logger;

void main() {

    try (Connection con = DriverManager.getConnection("jdbc:sqlite:test.db")) {

        try (Statement st = con.createStatement()) {

            st.addBatch("DROP TABLE IF EXISTS cars");
            st.addBatch("CREATE TABLE cars(id INTEGER PRIMARY KEY, name TEXT, price INT)");

            st.addBatch("INSERT INTO cars(name, price) VALUES('Audi',52642)");
            st.addBatch("INSERT INTO cars(name, price) VALUES('Mercedes',57127)");
            st.addBatch("INSERT INTO cars(name, price) VALUES('Skoda',9000)");
            st.addBatch("INSERT INTO cars(name, price) VALUES('Volvo',29000)");
            st.addBatch("INSERT INTO cars(name, price) VALUES('Bentley',350000)");
            st.addBatch("INSERT INTO cars(name, price) VALUES('Citroen',21000)");
            st.addBatch("INSERT INTO cars(name, price) VALUES('Hummer',41400)");
            st.addBatch("INSERT INTO cars(name, price) VALUES('Volkswagen',21600)");
            st.executeBatch();
        }

    } catch (SQLException ex) {

        Logger lgr = Logger.getLogger(getClass().getName());
        lgr.log(Level.SEVERE, ex.getMessage(), ex);
    }
}
```

## Retrieve data

```java

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.logging.Level;
import java.util.logging.Logger;

void main() {

    String query = "SELECT * FROM cars";

    try (Connection con = DriverManager.getConnection("jdbc:sqlite:test.db");
            PreparedStatement pst = con.prepareStatement(query);
            ResultSet rs = pst.executeQuery()) {

        while (rs.next()) {

            System.out.printf("%d %s %d%n", rs.getInt(1),
                    rs.getString(2), rs.getInt(3));
        }

    } catch (SQLException ex) {

        Logger lgr = Logger.getLogger(getClass().getName());
        lgr.log(Level.SEVERE, ex.getMessage(), ex);
    }
}
```

## Prepared statements 

When we write prepared statements, we use placeholders instead of directly writing the  
values into the statements. Prepared statements increase security and performance.  

A `PreparedStatement` is an object which represents a precompiled SQL statement.  

```java

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.util.logging.Level;
import java.util.logging.Logger;

void main() {

    int carPrice = 23999;
    String carName = "Oldsmobile";

    String sql = "INSERT INTO cars(name, price) VALUES(?, ?)";

    try (Connection con = DriverManager.getConnection("jdbc:sqlite:test.db")) {

        try (PreparedStatement pst = con.prepareStatement(sql)) {

            pst.setString(1, carName);
            pst.setInt(2, carPrice);
            pst.executeUpdate();

            System.out.println("A new car has been inserted");
        }

    } catch (SQLException ex) {

        Logger lgr = Logger.getLogger(getClass().getName());
        lgr.log(Level.SEVERE, ex.getMessage(), ex);
    }
}
```

When we write prepared statements, we use placeholders instead of directly writing the values  
into the statements. Prepared statements are faster and guard against SQL injection attacks.  
The `?` is a placeholder which is going to be filled later.  

## Metadata 

The following example shows how to print column headers with the data from the database table.   
We refer to column names as MetaData. MetaData is data about the core data in the database.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;
import java.sql.SQLException;
import java.util.logging.Level;
import java.util.logging.Logger;

void main() {

    String query = "SELECT * FROM cars";

    try (Connection con = DriverManager.getConnection("jdbc:sqlite:test.db");
            PreparedStatement pst = con.prepareStatement(query);
            ResultSet rs = pst.executeQuery()) {

        ResultSetMetaData meta = rs.getMetaData();

        String colName1 = meta.getColumnName(1);
        String colName2 = meta.getColumnName(2);
        String colName3 = meta.getColumnName(3);

        String header = String.format("%-8s %-21s %-15s%n", colName1, colName2, colName3);
        System.out.println(header);

        while (rs.next()) {

            System.out.printf("%-8s %-21s %-15d%n", rs.getInt(1),
                    rs.getString(2), rs.getInt(3));
        }

    } catch (SQLException ex) {

        Logger lgr = Logger.getLogger(getClass().getName());
        lgr.log(Level.SEVERE, ex.getMessage(), ex);
    }
}
```
