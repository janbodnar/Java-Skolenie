# Priklady

## Retrive table based on metadata

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
        int colCount = meta.getColumnCount();

        // Store column names and calculate maximum width for each column
        String[] colNames = new String[colCount];
        int[] colWidths = new int[colCount];

        // Get column names and initialize widths
        for (int i = 0; i < colCount; i++) {
            colNames[i] = meta.getColumnName(i + 1);
            colWidths[i] = colNames[i].length(); // Start with column name length
        }

        // Print column headers
        for (int i = 0; i < colCount; i++) {
            System.out.printf("%-" + (colWidths[i] + 2) + "s", colNames[i]);
        }
        System.out.println();

        // Print separator line
        for (int i = 0; i < colCount; i++) {
            System.out.printf("%-" + (colWidths[i] + 2) + "s", "-".repeat(colWidths[i]));
        }
        System.out.println();

        // Process each row
        while (rs.next()) {
            for (int i = 0; i < colCount; i++) {
                // Get column type to handle different data types
                int colType = meta.getColumnType(i + 1);
                String value;

                switch (colType) {
                    case java.sql.Types.INTEGER:
                    case java.sql.Types.BIGINT:
                        value = String.valueOf(rs.getInt(i + 1));
                        break;
                    case java.sql.Types.VARCHAR:
                    case java.sql.Types.CHAR:
                        value = rs.getString(i + 1) != null ? rs.getString(i + 1) : "";
                        break;
                    case java.sql.Types.DOUBLE:
                    case java.sql.Types.FLOAT:
                        value = String.format("%.2f", rs.getDouble(i + 1));
                        break;
                    case java.sql.Types.DATE:
                        value = rs.getDate(i + 1) != null ? rs.getDate(i + 1).toString() : "";
                        break;
                    default:
                        value = rs.getObject(i + 1) != null ? rs.getObject(i + 1).toString() : "";
                        break;
                }

                // Update column width if value is longer
                colWidths[i] = Math.max(colWidths[i], value.length());
                System.out.printf("%-" + (colWidths[i] + 2) + "s", value);
            }
            System.out.println();
        }

    } catch (SQLException ex) {
        Logger lgr = Logger.getLogger("MyLogger");
        lgr.log(Level.SEVERE, "SQLException occurred: " + ex.getMessage(), ex);
    } catch (Exception ex) {
        Logger lgr = Logger.getLogger("MyLogger");
        lgr.log(Level.SEVERE, "Unexpected error: " + ex.getMessage(), ex);
    }
}

```




## Prepared statements

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
//    String sql = "INSERT INTO cars(name, price) VALUES(" + carName + ", " + carPrice + ")";
//    String sql = String.format("INSERT INTO cars(name, price) VALUES(%s,%d"), carName, carPrice);


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



## Opakovanie 

```java

record User(String firstName, String lastName, String occupation) {

}

void main() {

    // find several ways how to print 'hello there' 7 times in Java in one line

    // create an array of 100 random values between 1, 100

    // flatten the array
    int[][] vals = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};


    // read the words.txt file and calculate the number of unique
    // words

    // calculate the number of apples
    // use regex
    String text = """
            there are 4 apples in the basket, 12 apples on the table
            and 9 apples in the fridge
            """;

    // filter out all gardeners
    // add date of birth attribute (a String) and calculate each users' age
    List<User> users = List.of(
            new User("John", "Doe", "gardener"),
            new User("Roger", "Roe", "driver"),
            new User("Alice", "Smith", "teacher"),
            new User("Bob", "Johnson", "engineer"),
            new User("Charlie", "Brown", "doctor"),
            new User("Dave", "Wilson", "chef"),
            new User("Emma", "Davis", "artist"),
            new User("Frank", "Miller", "musician"),
            new User("Grace", "Taylor", "nurse"),
            new User("Henry", "Anderson", "scientist"),
            new User("Isabella", "White", "gardener"),
            new User("Jack", "Harris", "firefighter"),
            new User("Katherine", "Martin", "pilot"),
            new User("Leo", "Thompson", "gardener"),
            new User("Mia", "Moore", "lawyer"),
            new User("Nathan", "Clark", "policeman"),
            new User("Olivia", "Lewis", "gardener"),
            new User("Peter", "Walker", "photographer"),
            new User("Quinn", "Hall", "programmer"),
            new User("Rachel", "Allen", "gardener")
    ); 
}
```

## Riesenia

```java
    // find several ways how to print 'hello there ' 7 times in Java in one line

    for (int i = 0; i<7; i++) {

        System.out.print("hello there ");
    }

    System.out.println();

    System.out.println("hello there ".repeat(7));

    System.out.println();

    String result = String.join("", Collections.nCopies(7, "hello there "));
    System.out.println(result);

    System.out.println();

    var sb = new StringBuilder();
    for (int i = 0; i<7; i++) {

        sb.append("hello there ");
    }

    System.out.println(sb);


    String output = Stream.generate(() -> "hello there ")
            .limit(7)
            .collect(Collectors.joining());

    System.out.println(output);


    int[] rvals = new int[100];

    var rand = new Random();

    for (int i = 0; i < 100; i++) {

        rvals[i] = rand.nextInt(100) + 1;
    }

    System.out.println(Arrays.toString(rvals));


    int[] rvals2 = rand.ints(100, 0, 100).toArray();
    System.out.println(Arrays.toString(rvals2));


    // flatten the array
    int[][] vals = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};

    int[] flattened = Arrays.stream(vals).flatMapToInt(Arrays::stream).toArray();
    System.out.println(Arrays.toString(flattened));

    String fileName = "words.txt";

    try (var lines = Files.lines(Path.of(fileName))) {
        long n = lines.distinct().count();
        System.out.println(n);
    }

    // user regex
    String text = """
            there are 4 apples in the basket, 12 apples on the table
            and 9 apples in the fridge and 34 pears on the floor.
            """;

    int totalApples = 0;

    var pattern = Pattern.compile("(\\d+) apples");
    Matcher matcher = pattern.matcher(text);

    while (matcher.find()) {
        totalApples += Integer.parseInt(matcher.group(1));
    }

    System.out.println(totalApples);



record User(String firstName, String lastName, String occupation, String dateOfBirth) {

    int age() {
        return Period.between(LocalDate.parse(dateOfBirth), LocalDate.now()).getYears();
    }

}

void main() throws IOException {


    // filter out all gardeners
    // add date of birth attribute (a String) and calculate each users' age
    List<User> users = List.of(
            new User("John", "Doe", "gardener", "2001-12-04"),
            new User("Roger", "Roe", "driver", "1995-08-22"),
            new User("Alice", "Smith", "teacher", "1987-06-13"),
            new User("Bob", "Johnson", "engineer", "1992-11-30"),
            new User("Charlie", "Brown", "doctor", "1985-09-14"),
            new User("Dave", "Wilson", "chef", "1998-04-27"),
            new User("Emma", "Davis", "artist", "1991-03-08"),
            new User("Frank", "Miller", "musician", "1989-07-19"),
            new User("Grace", "Taylor", "nurse", "1996-10-05"),
            new User("Henry", "Anderson", "scientist", "1984-12-01"),
            new User("Isabella", "White", "gardener", "2000-02-17"),
            new User("Jack", "Harris", "firefighter", "1993-05-21"),
            new User("Katherine", "Martin", "pilot", "1988-08-09"),
            new User("Leo", "Thompson", "gardener", "1999-07-04"),
            new User("Mia", "Moore", "lawyer", "1994-11-11"),
            new User("Nathan", "Clark", "policeman", "1997-01-23"),
            new User("Olivia", "Lewis", "gardener", "1986-06-29"),
            new User("Peter", "Walker", "photographer", "1990-09-16"),
            new User("Quinn", "Hall", "programmer", "1983-04-12"),
            new User("Rachel", "Allen", "gardener", "1995-02-28")
    );

    users.forEach(user -> System.out.println(user.age()));

    List<User> filtered = new ArrayList<>();
    for (var user : users) {

        if ("gardener".equals(user.occupation())) {
            filtered.add(user);
        }
    }

    System.out.println(filtered);

    var gardeners = users.stream().filter(user -> "gardener".equals(user.occupation)).toList();
    System.out.println(gardeners);

}

```






## Regex split

```java
void main() {

    String data = "1,2,3;4,5;6,7;8,9;10";

    String[] fields = data.split("[,;]");

    List<Integer> vals = Arrays.stream(fields).map(Integer::parseInt).toList();

    System.out.println(Arrays.toString(fields));
    System.out.println(vals);
}
```


## Regex groups

```java
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    var sites = List.of("Paul Novak:gardener", "Kate Smith:singer", "Paul Black:programmer",
            "Arkadij Novy:student");

    Pattern p = Pattern.compile("(\\w+):(\\w+)");

    List<String> jobs = new ArrayList<>();

    for (var site: sites) {

        Matcher matcher = p.matcher(site);

        while (matcher.find()) {

            jobs.add(matcher.group(2));
        }
    }
    System.out.println(jobs);
}
```


## GUI APP

```java
package com.zetcode;

import javax.swing.GroupLayout;
import javax.swing.JButton;
import javax.swing.JComponent;
import javax.swing.JFrame;
import java.awt.EventQueue;

public class QuitButtonEx extends JFrame {

    public QuitButtonEx() {

        initUI();
    }

    private void initUI() {

        var quitButton = new JButton("Quit");
        quitButton.addActionListener(_ -> System.exit(0));

        createLayout(quitButton);

        setTitle("Quit button");
        setSize(400, 300);
        setLocationRelativeTo(null);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
    }

    private void createLayout(JComponent... arg) {

        var pane = getContentPane();
        var gl = new GroupLayout(pane);
        pane.setLayout(gl);

        gl.setAutoCreateContainerGaps(true);

        gl.setHorizontalGroup(gl.createSequentialGroup()
                .addComponent(arg[0])
        );

        gl.setVerticalGroup(gl.createSequentialGroup()
                .addComponent(arg[0])
        );
    }

    public static void main(String[] args) {

        EventQueue.invokeLater(() -> {

            var ex = new QuitButtonEx();
            ex.setVisible(true);
        });
    }
}
```



## Parse last 3 countries

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

void main() throws IOException {

    String url = "https://webcode.me";
    Document document = Jsoup.connect(url).get();

    String cssQuery = "body p:nth-of-type(2)";
    var tag = document.select(cssQuery).first();

    System.out.println(tag);

    String url2 = "https://webcode.me/countries.html";
    Document document2 = Jsoup.connect(url2).get();

    String cssQuery2 = "table tbody tr:nth-last-child(-n+3)";
    var last3Rows = document2.select(cssQuery2);

    System.out.println(last3Rows);
}
```


## HTML/CSS


```css
h1 {
    color: blue;
    font-size: 5em;
    text-align: center;
}

p:first-child {
    font-size: 2em;
    text-align: center;
    color: red;
}

p:last-child {
    font-size: 1.5em;
    text-align: center;
    color: green;
}

footer p {
    font-size: 1.2em;
    text-align: center;
    color: purple;
}
```

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="style.css">
</head>

<body>

    <h1>My First Heading</h1>


    <p font="">My first paragraph.</p>

    <ul>
        <li>sky</li>
        <li>auto</li>
        <li>red</li>
        <li>past</li>
        <li>word</li>
        <li>rock</li>
        <li>pen</li>
        <li>dog</li>
        <li>cat</li>
        <li>mouse</li>
    </ul>

    <p>My second paragraph.</p>


    <footer>
        <p>My first footer.</p>
        <p>My second footer.</p>
        <p>My third footer.</p>
        <p>My fourth footer.</p>
        <p>My fifth footer.</p>
    </footer>

</body>

</html>
```











## JSoup

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

void main() throws IOException {

    String url = "https://webcode.me";
    Document doc = Jsoup.connect(url).get();

    String title = doc.title();
    System.out.println(title);

    System.out.println("------------------------------");
    
    var body = doc.body();
    System.out.println(body);
    System.out.println(body.tagName());
    System.out.println(body.text());

    System.out.println("------------------------------");
    var children = body.children();

    children.forEach(System.out::println);
}
```









## Opakovanie

The `words.txt` file:

```
sky
blue
word
war
rock
blue
jean
nice
alcohol
post
rock
flower
sweater
```



```java
void main() {

    // calculate sum
// create a copy 
    int[] vals = {3, 2, 2, 2, 1, 1, 3, 6, 7, 8, 9};


//    filter all words with 3 letters
//    filter all words starting with 'w'
//    sort words in ascending and descending modes
    List<String> words = List.of("sky", "blue", "job",
            "rock", "cup", "club", "atom", "water", "war");


    // calculate sum
    String data = """
            1,2,3,4,5
            6,7,8,9,10
            """;

    // select unique values
    int[] vals2 = {3, 2, 2, 2, 1, 1, 3, 6, 7, 8, 9};
    
    
//    print today's datetime (use copilot)
//    calculate age from "2001-11-28" (use copilot)

// read words.txt file and filter out words starting in 'w'
// read words.txt file and filter out words that contain 'w' letter
}
```

## Riesenia

```java
   // calculate sum
    int[] vals = {3, 2, 2, 2, 1, 1, 3, 6, 7, 8, 9};

    int sum = 0;

    for (int val: vals) {
        sum += val;
    }

    System.out.println(sum);

    int i = 0;
    int sum2 = 0;

    while (i < vals.length) {
        sum2 += vals[i];
        i++;
    }

    System.out.println(sum2);


    int sum = 0;

    for (int val: vals) {
        sum += val;
    }

    System.out.println(sum);

    int i = 0;
    int sum2 = 0;

    while (i < vals.length) {
        sum2 += vals[i];
        i++;
    }

    System.out.println(sum2);

    int sum3 = Arrays.stream(vals).sum();
    System.out.println(sum3);


    int[] vals_copy = Arrays.stream(vals).toArray();
    System.out.println(Arrays.toString(vals_copy));

    int[] vals_copy2 = Arrays.copyOf(vals, vals.length);
    System.out.println(Arrays.toString(vals_copy2));


//    filter all words with 3 letters
//    filter all words starting with 'w'
//    sort words in ascending and descending modes
    List<String> words = List.of("sky", "blue", "job",
            "rock", "cup", "club", "atom", "water", "war");

    words.stream().filter(word -> word.startsWith("w")).forEach(System.out::println);
    words.stream().filter(word -> word.length() == 3).forEach(System.out::println);

    List<String> sorted_asc = words.stream().sorted().toList();
    System.out.println(sorted_asc);

    List<String> sorted_desc = words.stream().sorted(Comparator.reverseOrder()).toList();
    System.out.println(sorted_desc);


//    List<String> words_3 = new ArrayList<>();
//
//    for (var word : words) {
//        if (word.startsWith("w")) {
//            words_3.add(word);
//        }
//    }
//
//    System.out.println(words_3);

    // select unique values
    int[] vals2 = {3, 2, 2, 2, 1, 1, 3, 6, 7, 8, 9};

    int[] uvals = Arrays.stream(vals2).distinct().toArray();
    System.out.println(Arrays.toString(uvals));


    var now = LocalDate.now();
    System.out.println(now);

    String dateOfBirthS = "2001-11-28";
    LocalDate dob = LocalDate.parse(dateOfBirthS);
    
    int years = Period.between(dob, now).getYears();
    System.out.println(years);


    // calculate sum
    String data = """
            1,2,3,4,5
            6,7,8,9,10
            """;

    int sum = 0;
    for (String line : data.split("\\n")) {
        for (String num : line.split(",")) {
            sum += Integer.parseInt(num);
        }
    }

    System.out.println("Sum: " + sum);


    int sum2 = 0;
    List<String> lines = data.lines().toList();

    for (String line: lines) {
        String[] fields = line.split(",");
        for (String field: fields) {
            sum2 += Integer.parseInt(field);
        }
    }

    System.out.println(sum2);

// read words.txt file and filter out words starting in 'w'
// read words.txt file and filter out words that contain 'w' letter

    Files.readAllLines(Path.of("words.txt")).stream()
            .filter(line -> line.startsWith("w"))
            .forEach(System.out::println);

    Files.readAllLines(Path.of("words.txt")).stream()
            .filter(line -> line.contains("w"))
            .forEach(System.out::println);
```













## Optional with Streams

```java
void main() {

    Stream<String> colours = Stream.of("red", "green", "blue", "yellow", "orange", "pink");

    Optional<String> first = colours.skip(4).findFirst();
    first.ifPresent(System.out::println);

    Stream<Integer> nums = Stream.of(3, 4, 5, 6, 7);
    Optional<Integer> maxVal = nums.max(Comparator.naturalOrder());
    maxVal.ifPresent(e -> System.out.println(2 * e));

    nums = Stream.of(3, 4, 5, 6, 7);
    Optional<Integer> minVal = nums.min(Comparator.naturalOrder());
    minVal.ifPresent(System.out::println); 
}
```


## Multiple inheritance

```java
package com.zetcode;

abstract class Shape {

    protected int x;
    protected int y;

    public abstract double area();
}

class Rectangle extends Shape {

    public Rectangle(int x, int y) {

        this.x = x;
        this.y = y;
    }

    @Override
    public double area() {

        return this.x * this.y;
    }
}

class Circle extends Shape {

    private int radius;

    public Circle(int radius) {
        this.radius = radius;
    }

    @Override
    public double area() {
        return this.radius * this.radius * Math.PI;
    }
}

class Square extends Shape {

    public Square(int x) {

        this.x = x;
    }

    @Override
    public double area() {

        return this.x * this.x;
    }
}

public class Main {

    public static void main(String[] args) {

        Circle[] circles = {new Circle(5), new Circle(8), new Circle(11), new Circle(12)};
        Shape[] shapes = { new Square(5), new Circle(10), new Rectangle(9, 4), new Square(12) };

        for (Shape shape : shapes) {

            System.out.println(shape.area());
        }
    }
}
```


## Program


```java
package com.example;

import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.Random;

public class Program {
    
    public void run() {

        print100RandomInts();
        
        System.out.println(now());
        System.out.println(now());
    }

    private void print100RandomInts() {

        var rand = new Random();
        
        for (int i = 0; i<100; i++) {

            System.out.println(rand.nextInt(100));
        }
    }

    private String now() {

        LocalDateTime now = LocalDateTime.now();
        DateTimeFormatter formatter = DateTimeFormatter.ISO_DATE_TIME;

        return now.format(formatter);
    }
}
```




The `words.txt` file:

```
sky
ocean
pup
rock
war
water
small
```


```java
import java.util.Random;

void main(String ... args) {

    // calculate min, max, sum, avg of salaries

    HashMap<String, Integer> salaries = new HashMap<>();

    salaries.put("emp1", 2300);
    salaries.put("emp2", 1350);
    salaries.put("emp3", 4100);
    salaries.put("emp4", 2100);
    salaries.put("emp5", 2900);
    salaries.put("emp6", 1380);
    

    // create a list of 100 random integers from 1 .. 100


    // create int[] vals3 from

    int[] vals = {1, 2, 3};
    int[] vals2 = {4, 5, 6};


    // Read data from words.txt and print
    // in uppercase


    // load data into list and sort it

    String data = """
            small,new,purple
            big,cup,nest
            data,cloud,ink
            """;
 
}
```

## Riesenia

```java
    List<Integer> randomVals = new ArrayList<>();
    Random rand = new Random();

    for (int i = 0; i < 100; i++) {

        int r = rand.nextInt(1, 100);
        randomVals.add(r);
    }

    System.out.println(randomVals);

    // ---------

    int[] original = {1, 2, 3, 4, 5, 6};
    int[] newArray = new int[original.length];

    for (int i=0; i<original.length;i++) {
        newArray[i]  = original[i];
    }

    System.out.println(Arrays.toString(newArray));
    
    int[] copy = Arrays.copyOf(original, original.length);
    System.out.println(Arrays.toString(copy));

    // -------

    List<String> lines = Files.readAllLines(Paths.get("words.txt"));
    lines.forEach(line -> System.out.println(line.toUpperCase()));

    // -------

    String data = """
            small,new,purple
            big,cup,nest
            data,cloud,ink
            """;

    List<String> lines = data.lines().toList();
    System.out.println(lines);

    for (String line: lines) {
        System.out.println(line);
    }

    // -------

    HashMap<String, Integer> salaries = new HashMap<>();

    salaries.put("emp1", 2300);
    salaries.put("emp2", 1350);
    salaries.put("emp3", 4100);
    salaries.put("emp4", 2100);
    salaries.put("emp5", 2900);
    salaries.put("emp6", 1380);

    int sum = 0;
    int min = 0;
    int max = 0;

    var values = salaries.values();
    min = Integer.MAX_VALUE;

    for (int value: values) {

        if (value > max) {
            max = value;
        }

        if (value < min) {
            min = value;
        }

        sum += value;
    }

    System.out.println(sum);
    System.out.println(max);
    System.out.println(min);
    System.out.println(sum/values.size());

    // -------

    HashMap<String, Integer> salaries = new HashMap<>();

    salaries.put("emp1", 2300);
    salaries.put("emp2", 1350);
    salaries.put("emp3", 4100);
    salaries.put("emp4", 2100);
    salaries.put("emp5", 2900);
    salaries.put("emp6", 1380);

    var values = salaries.values();
    
    int min = Collections.min(values);
    int max = Collections.max(values);

    System.out.println(min);
    System.out.println(max);

    int sum = 0;

    for (int value: values) {

        sum += value;
    }

    System.out.println(sum);
    System.out.println(sum/values.size());
```



## Looping Hashmaps

```java
import java.util.HashMap;
import java.util.Map;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    capitals.forEach((k, v) -> {
                if (v.startsWith("B") || v.startsWith("W")) {
                    System.out.printf("%s - %s%n", k, v);
                }
            }
    );
}
```


```java
import java.util.HashMap;
import java.util.Map;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    for (var pair: capitals.entrySet()) {

        if (pair.getValue().endsWith("e")) {
            System.out.println(pair);
        }

//        System.out.format("%s: %s%n", pair.getKey(), pair.getValue());
    }
}
```



## Contains key/value

```java
import java.util.HashMap;
import java.util.Map;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    String key1 = "ger";
    String key2 = "rus";

    String value1 = "Trnava";

    if (!capitals.containsValue(value1)) {
        System.out.println("Hashmap does not contain value " + value1);
    } else {
        System.out.println("Hashmap does contain value " + value1);
    }


    if (capitals.containsKey(key1)) {

        System.out.printf("HashMap contains %s key%n", key1);
    } else {

        System.out.printf("HashMap does not contain %s key%n", key1);
    }

    if (capitals.containsKey(key2)) {

        System.out.printf("HashMap contains %s key%n", key2);
    } else {

        System.out.printf("HashMap does not contain %s key%n", key2);
    }
}
```



## Reading files

```java
void main() throws IOException {

//    String fileName = "words.txt";
//    String fileName = "C:/Users/bodnar//IdeaProjects/SimpleEx/words.txt";
//    String fileName = "C:\\Users\\bodnar\\IdeaProjects\\SimpleEx\\words.txt";

    String fileName = "C:/Users/bodnar/Documents/words.txt";

    List<String> lines = Files.readAllLines(Paths.get(fileName));
    lines.forEach(line -> System.out.println(line.toUpperCase()));

    for (String line: lines) {
        System.out.println(line.length());
    }


//    String content = Files.readString(Paths.get(fileName));
//
//    System.out.println(content);
//    String[] words = content.split("[\\s]+");

//    System.out.println(Arrays.toString(words));

}
```


## forEach loop

```java
void main() {

    List<String> words = List.of("sky", "blue", "cup", "ocean");

    words.forEach(word -> System.out.println(word.toUpperCase()));

    for (String word : words) {
        System.out.println(word.toUpperCase());
    }

}
```




## Sorting arrays

```java
import java.util.Arrays;

void main() {

    int[] a = { 5, 2, 4, 3, 1 };
    int[] sorted = Arrays.stream(a).sorted().toArray();

    System.out.println(Arrays.toString(sorted));
    System.out.println(Arrays.toString(a));

    int[] b = { 5, 2, 4, 3, 1 };
    Arrays.sort(b);
    System.out.println(Arrays.toString(b));
}
```


## Split with regex

```java
void main(String[] args) {

     // calculate sum
    String data2 = "1,2;3,4;5,6,7;8,9;10";
    int sum3 = 0;

    String[] fields = data2.split("[;,]");

    for (String field: fields) {

        sum3 += Integer.parseInt(field);
    }

    System.out.println(sum3);
}
```


## Replace and calculate

```java
void main(String[] args) {

     // calculate sum
    String data2 = "1,2;3,4;5,6,7;8,9;10";
    int sum3 = 0;

    String cleanedData = data2.replace(';', ',');
    
    String[] fields = cleanedData.split(",");

    for (String field: fields) {

        sum3 += Integer.parseInt(field);
    }

    System.out.println(sum3);

}
```





## Opakovanie

```java
void main(String[] args) {

    // print message: John Doe is 34 years old, he is a gardener
    String name = "John Doe";
    int age = 34;
    String occupation = "gardener";

    // calculate sum using for loop
    // print first, second, last, last but one elements
    var vals = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
    // calculate sum of values 20..50, both inclusive
    // using while loop

    // print first, second, last, last but one element
    int[] data = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

    // calculate sum
    String data2 = "1,2,3,4,5,6,7,8,9,10";

}
```


## Riesenia

```java
    // print message: John Doe is 34 years old, he is a gardener
    String name = "John Doe";
    int age = 34;
    String occupation = "gardener";

    System.out.printf("%s is %d years old, he is a %s%n", name, age, occupation);

    String msg = String.format("%s is %d years old, he is a %s%n", name, age, occupation);
    System.out.println(msg);

    // calculate sum using for loop
    // print first, second, last, last but one elements
    List<Integer> vals = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

    int sum = 0;

    for (Integer val: vals) {
        sum += val;
    }

    System.out.println(sum);
    
    int first = vals.getFirst();
    int second = vals.get(1);
    int last = vals.getLast();
    int lastButOne = vals.get(vals.size() - 2);

    System.out.println(first);
    System.out.println(second);
    System.out.println(last);
    System.out.println(lastButOne);


    // calculate sum of values 20..50, both inclusive
    // using while loop

    int sum2 = 0;
    int i = 20;

    while (i <= 50) {

        sum2 += i;
        i++;
    }

    System.out.println(sum2);


    // print first, second, last, last but one element
    int[] data = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

    System.out.println(data[0]);
    System.out.println(data[1]);
    System.out.println(data[data.length - 1]);
    System.out.println(data[data.length - 2]);


     // calculate sum
    String data2 = "1,2,3,4,5,6,7,8,9,10";
    int sum3 = 0;
    
    String[] fields = data2.split(",");

    for (String field: fields) {

        sum3 += Integer.parseInt(field);
    }

    System.out.println(sum3);

```
















## Calculate sum of CSV data

```java
void main(String[] args) {

//   1. calculate sum
//   2. transform to 1;2;3;4;5;6;7;8;9;10
    String data = "1,2,3,4,5,6,7,8,9,10";

//    ["1", "2", .. "10"]
    String[] fields = data.split(",");
    int sum = 0;

    for (String field :fields) {
        sum += Integer.parseInt(field);
    }

    System.out.println(sum);

}
```


## Sum of program args

```java
void main(String[] args) {

    int sum = 0;

    for (String arg : args) {
        sum += Integer.parseInt(arg);
    }

    System.out.println(sum);
}
```


## split function

```java
void main() {

    String fullName = "John Doe";

    String[] parts = fullName.split(" ");

    String firstName = parts[0];
    String lastName = parts[1];

    System.out.println(firstName);
    System.out.println(lastName);

    System.out.println(fullName);
}
```


## and/or operators

```java
void main() {

    String[] words = {"war", "water", "cup", "snow", "pup", "cloud", "dog", "warm"};
    
    for (var word : words) {

        if (word.startsWith("w") || word.startsWith("c")) {
            System.out.println(word);
        }

        if (word.length() == 3 && word.startsWith("w")) {
            System.out.println(word);
        }
    }
}
```



## Opakovanie

```java
void main() {

    // print message John Doe is 45 years old
    String name = "John Doe";
    int age = 45;
    
    // calculate sum of 1..10 integers
    int[] vals = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    
    // print the following message 8 times using while loop
    String msg = "an old falcon";
    
    // print first, last, last but one elements
    // calculate the sum of lenghts
    String[] words = {"sky", "look", "pen", "snow", "car", "war"};
    
    // using classic for loop, generate 10 random numbers
    var random = new Random();
}
```

## Riesenia

```java
void main() {

    // print message John Doe is 45 years old
    String name = "John Doe";
    int age = 45;

    System.out.printf("%s is %d years old%n", name, age);
    System.out.println(name + " is " + age + " years old");

    // calculate sum of 1..10 integers
    int[] vals = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int sum = 0;

    for (int val : vals) {
        sum = sum + val;
    }

    System.out.println(sum);

    // print the following message 8 times using while loop
    String msg = "an old falcon";

    for (int i = 0; i < 8; i++) {
        System.out.println(msg);
    }

    int i = 0;

    while (i < 8) {
        System.out.println(msg);
        i++;
    }

    System.out.println("end of program");


    String[] words = {"sky", "look", "pen", "snow", "car", "war"};

    int len = words.length;

    System.out.println(words[0]);
    System.out.println(words[len-1]);
    System.out.println(words[len-2]);

    int sum_of_chars = 0;

    for (String word : words) {
        sum_of_chars += word.length();
    }

    System.out.println(sum_of_chars);

    System.out.println("end of program");

    // using classic for loop, generate 10 random numbers
    var random = new Random();

    for (int i = 0; i<10; i++) {

        int r = random.nextInt();
        System.out.println(r);
    }

}
```











## toString funkcia

```java
package com.zetcode;

class Person {

    public String firstName;
    public String lastName;
    public String occupation;

    @Override
    public String toString() {
        return "Person{" +
                "firstName='" + firstName + '\'' +
                ", lastName='" + lastName + '\'' +
                ", occupation='" + occupation + '\'' +
                '}';
    }
}

public class Main {

    public static void main(String[] args) {

        Person p1 = new Person();
        p1.firstName = "Jane";
        p1.lastName = "Doe";
        p1.occupation = "teacher";

        Person p2 = new Person();
        p2.firstName = "Roger";
        p2.lastName = "Roe";
        p2.occupation = "driver";

        System.out.println(p1);
        System.out.println(p2);

    }
}
```


## Map of planets

```java
void main() {

    Map<String, Double> planetDistances = new HashMap<>();

    // Adding planets and their distances from the Sun
    planetDistances.put("Mercury", 57.9);
    planetDistances.put("Venus", 108.2);
    planetDistances.put("Earth", 149.6);
    planetDistances.put("Mars", 227.9);
    planetDistances.put("Jupiter", 778.3);
    planetDistances.put("Saturn", 1427.0);
    planetDistances.put("Uranus", 2871.0);
    planetDistances.put("Neptune", 4497.1);

    // Printing the map
    planetDistances.forEach((planet, distance) ->
            System.out.println(planet + ": " + distance + " million km")
    );
}
```

## Fill arrays

```java
import java.util.Arrays;

void main() {

    int[] a = new int[10];

    System.out.println(Arrays.toString(a));
    Arrays.fill(a, 1);

    System.out.println(Arrays.toString(a));

    double[] b = new double[15];
    Random r = new Random();
    Arrays.setAll(b, idx -> r.nextDouble(10));

    System.out.println(Arrays.toString(b));

    float[] b2 = new float[15];
    Random r1 = new Random();

    for (int i = 0; i < b2.length; i++) {
        float randomFloat = r.nextFloat() * 100; // Generate a random float between 0 and 100
        float roundedFloat = Math.round(randomFloat * 100.0f) / 100.0f; // Round to two decimal places
        b2[i] = roundedFloat;
    }
    
    System.out.println(Arrays.toString(b2));
}
```

## Read CSV file

```java
void main() throws IOException {

    String fileName = "C:/Users/bodnar/Documents/data.csv";
    Path filePath = Path.of(fileName);

    List<String> lines = Files.readAllLines(filePath);

    int suma = 0;

    for (String line : lines) {

        String[] fields = line.split(";");


        for (String field : fields) {
            suma = suma + Integer.parseInt(field);
        }
    }

    System.out.println(suma);
}
```


## Suma z CSV dat

```java
void main() {

    String data = "1,2,3,4,5,6,7,8,9,10";
    String[] fields = data.split(",");

    int suma = 0;

    for (String field : fields) {
        suma = suma + Integer.parseInt(field);
    }

    System.out.println(suma);
```


## Stranky na riesenie uloh

- [leetcode.com](https://leetcode.com/)
- [www.codewars.com](https://www.codewars.com/)


## Frekvencia znakov v texte

```java
void main() {

    String text = """
            The Battle of Thermopylae was fought between an alliance of Greek city-states,
            led by King Leonidas of Sparta, and the Persian Empire of Xerxes I over the
            course of three days, during the second Persian invasion of Greece.
            """;

    Map<Character, Integer> charCountMap = new HashMap<>();

    for (char c : text.toCharArray()) {
        if (charCountMap.containsKey(c)) {
            charCountMap.put(c, charCountMap.get(c) + 1);
        } else {
            charCountMap.put(c, 1);
        }
    }

    charCountMap.forEach((key, value) -> System.out.println(key + ": " + value));
}
```


## Cleaning words

```java
import java.util.List;

void main() {

    var words = List.of("sky\n", "\nwar\n", "toy  ", "  blue", "\t\t", "", "sky");
    System.out.println(words);

    ArrayList<String> words_cleaned = new ArrayList<>();

    for (String word : words) {

        if (!word.isBlank()) {
            words_cleaned.add(word.trim());
        }
    }

    System.out.println(words_cleaned);
}
```


## Ternary operator

```java
void main() {
    int age = 31;

    boolean adult = age >= 18 ? true : false;
    
//    if (age >= 18) {
//        adult = true;
//    } else {
//        adult = false;
//    }

    System.out.println(String.format("Adult: %s", adult));
}
```

## suma a dnesny datum

```java
void main() {

    // vypocitaj sumu
    int[] vals = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

    int sum = 0;

    for (int val : vals) {
        sum = sum + val;
    }

    System.out.println(sum);
    System.out.println(Arrays.stream(vals).sum());

    // Vypis dnesny datum

    LocalDate today = LocalDate.now();
    System.out.println("Dnešný dátum je: " + today);

}
```

## forEach funkcia

```java
void main() {

    // vypis slova zacinajuce sa na w
    // vypis slova majuce tri pismena
    List<String> words = List.of("sky", "blue", "water", "nord", "small", "war");

    words.forEach(w -> {
        if (w.startsWith("w")) {
            System.out.println(w);
        }
    });

    words.forEach(w -> {
        if (w.length() == 3) {
            System.out.println(w);
        }
    });
}
```


## Opakovanie

```java
void main() {

    // vypis hlasku John Doe is 45 years old and he is a gardener
    String name = "John Doe";
    int age = 45;
    String occupation = "gardener";


    // vypis slova zacinajuce sa na w
    // vypis slova majuce tri pismena
    List<String> words = List.of("sky", "blue", "nord", "small", "war");

    // vypocitaj sumu
    int[] vals = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};   
}
```



## Podmienene vypisanie hodnot pola

```java
void main() {

    String[] planets = {
            "Mercury", "Venus", "Earth",
            "Mars", "Jupiter", "Saturn", "Uranus", "Pluto"
    };

// Vypis planety zacinajuce na M alebo S
    for (String planet : planets) {

        if (planet.startsWith("M") || planet.startsWith("S") ) {
            System.out.println(planet);
        }
    }
}
```



## Sum array of integers 

```java
void main() {

    int[] vals = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

//    System.out.println(vals[0]);
//    System.out.println(vals[1]);
//    System.out.println(vals[2]);
//
//    System.out.println(vals[vals.length-1]);

    int vals_len = vals.length;

    int sum = 0;

    for (int i = 0; i < vals_len; i++) {

        sum = sum + vals[i];
    }

    System.out.println(sum);
}
```


## Random vals

```java
import java.util.Random;

void main() {

    var r = new Random();
    int num = r.nextInt(7) - 3;

    if (num > 0) {

        System.out.println("The number is positive");
    } else if (num < 0) {

        System.out.println("The number is negative");
    } else {
        System.out.println("The number is zero");
    }

//    if (num < 0) {
//        System.out.println("The number is negative");
//    }
//
//    if (num == 0) {
//        System.out.println("The number is zero");
//    }

}
```


## Program

```java
package me.webcode;

import java.util.List;

public class Program {

    void main() {

        List<String> words = List.of("sky", "storm");

        for (String word : words) {
            System.out.println(word);
        }

        int x = 10;
        int y = 11;
        int z = x + y;

        System.out.println(z);
    }
}
```


## Get ages of users

```java
import org.jdbi.v3.core.Jdbi;
import org.jdbi.v3.core.mapper.reflect.ConstructorMapper;

import java.util.List;

void main() {

    String jdbcUrl = "jdbc:postgresql://localhost:5432/testdb";
    String username = "postgres";
    String password = "postgres";

    Jdbi jdbi = Jdbi.create(jdbcUrl, username, password);

    List<User> users = jdbi.withHandle(handle -> handle.select("SELECT * FROM users")
            .registerRowMapper(User.class, ConstructorMapper.of(User.class))
            .mapTo(User.class)
            .list());

    if (users.isEmpty()) {

        System.out.println("No users found.");
    } else {

        System.out.println("found " + users.size() + " users");
    }

    for (User user: users) {

        LocalDate currentDate = LocalDate.now();
        LocalDate birthDate = LocalDate.parse(user.dob);
        Period age = Period.between(birthDate, currentDate);

        System.out.printf("%s %s is %d years old%n", user.first_name, user.last_name, age.getYears());
    }
}

public record User(int id, String first_name, String last_name, String occupation, String dob) {
}
```


```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="format.css">
    <title>My html page</title>
</head>
<body>

<a href="https://wikipedia.org">Wikipedia.org</a>

<p>Today is a beautiful day. We go swimming and fishing.</p>
<p>Hello there. How are you?</p>

<a href="https://youtube.com">Youtube</a>

</body>
</html>
```


## Get h1 from webpage

```java
package com.zetcode;

import java.io.IOException;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;

public class JSoupMetaInfoEx {

    public static void main(String[] args) throws IOException {

        String url = "https://wikipedia.sk";
        Document document = Jsoup.connect(url).get();

        Element h1tag = document.select("h1").first();

        if (h1tag != null) {
            String h1text = h1tag.text();
            System.out.println(h1text);
        } else {
            System.out.println("h1 tag not found");
        }
    }
}
```

## Regex 

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Optional;
import java.util.OptionalDouble;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main () {
    
    // calculate sum
    
    String data = """
            1;2;12,  4,5 ,6,  7;2;3
            1;2;6; 15;2;5;6;7;34
            """;

    Pattern pattern = Pattern.compile("[,;\\s]+");

    int suma = pattern.splitAsStream(data).mapToInt(Integer::valueOf).sum();
    System.out.println(suma);
    
    // calculate average
    String data2 = """
            | Jozef Novak 1230 |
            | John Doe 2340    |
            | Paul Smith 1234  |
            | Lucia Novak 1224 |
            """;

    Pattern pattern2 = Pattern.compile("\\d+");

    Matcher matcher = pattern2.matcher(data2);

    List<Integer> values = new ArrayList<>();

    while (matcher.find()) {
        int val = Integer.parseInt(matcher.group());
        values.add(val);
    }

    System.out.println(values);

    OptionalDouble avg = values.stream().mapToDouble(Double::valueOf).average();
    avg.ifPresent(System.out::println);


    // pick phrases that contain dog, falcon or night
    
    String data3 = """
            a new coin
            an old falcon
            a small house
            a stormy night
            a new costume
            a happy dog
            """;

//    Pattern pattern = Pattern.compile("dog|falcon|night");
//    List<String> found = data3.lines().filter(word -> pattern.matcher(word).find()).toList();
    List<String> found = data3.lines().filter(word -> word.matches(".* dog|.* falcon|night")).toList();
    System.out.println(found);
}
```


## Recap

```java
void main () {

    String data = """
            1;2;12,4,5,6,7;2;3
            1;2;6;15;2;5;6;7;34
            """;

    // compute sum of values

    String data2 = """
            | Jozef Novak 1230 |
            | John Doe 2340    |
            | Paul Smith 1234  |
            | Lucia Novak 1224 |
            """;

    // Compute average

    String data3 = """
            a new coin
            an old falcon
            a small house
            a stormy night
            a new costume
            a happy dog
            """;
    
    // pick phrases that contain dog, falcon or night

}
```

## Get date from JSON

```java
import com.google.gson.Gson;

import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;


void main() throws IOException, InterruptedException {

    String webPage = "http://time.jsontest.com";
    URI uri = URI.create(webPage);

    try (HttpClient client = HttpClient.newHttpClient()) {

        HttpRequest request = HttpRequest.newBuilder(uri).GET().build();
        String body = client.send(request, HttpResponse.BodyHandlers.ofString()).body();

        Gson gson = new Gson();
        TimeData td = gson.fromJson(body, TimeData.class);

        System.out.println(td);
    }
}

record TimeData(String time, Long milliseconds_since_epoch, String date) {
}
```


```json
[
  {
    "firstName": "John",
    "lastName": "Doe",
    "occupation": "gardener"
  },
  {
    "firstName": "Roger",
    "lastName": "Roe",
    "occupation": "teacher"
  },
  {
    "firstName": "Paul",
    "lastName": "Novak",
    "occupation": "programmer"
  }
]
```


## Json

```java
import com.google.gson.Gson;

void main() {

    Map<Integer, String> colours = new HashMap<>();
    colours.put(1, "blue");
    colours.put(2, "yellow");
    colours.put(3, "green");

    Gson gson = new Gson();
    String output = gson.toJson(colours);
    System.out.println(output);

    List<String> words = List.of("sky", "blue", "atom");

    String output2 = gson.toJson(words);
    System.out.println(output2);

    List<User> users = List.of(new User("John", "Doe", "gardener"),
            new User("Roger", "Roe", "teacher"),
            new User("Paul", "Novak", "programmer"));

    String output3 = gson.toJson(users);
    System.out.println(output3);

}

record User(String firstName, String lastName, String occupation) {
}
```


## Filter nulls

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    List<String> words = new ArrayList<>() {{
        add("sky");
        add(null);
        add("blue");
        add(null);
        add("cloud");
        add(null);
        add("ocean");
    }};

    List<String> cleaned = words.stream().filter(word -> word != null).toList();

    cleaned.forEach(word -> {
        System.out.printf("The %s word has %d letters%n", word, word.length());
    });
}
```

## Regex words from web

```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
import java.util.stream.Stream;

void main() throws IOException, InterruptedException {

    var uri = URI.create("https://www.mit.edu/~ecprice/wordlist.10000");

    try (HttpClient client = HttpClient.newHttpClient()) {

        HttpRequest request = HttpRequest.newBuilder(uri).GET().build();
        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

        Pattern pattern = Pattern.compile(".{10}");
        String body = response.body();

        List<String> lines = body.lines().toList();
        List<String> found = new ArrayList<>();

        for (String line : lines) {
            Matcher m = pattern.matcher(line);

            if (m.matches()) {
                found.add(line);
            }
        }

        System.out.println(found.size());

        Path path = Path.of("src/resources/words_10.txt");
        Files.write(path, found);

//        Path path = Path.of("src/resources/words.txt");
//        Files.writeString(path, body);

    }
}
```


## Regex, extrahovanie dat

```java
import java.util.ArrayList;
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    var sites = List.of("webcode.me", "zetcode.com", "freebsd.org", "netbsd.org");

    List<String> topLevels = new ArrayList<>();
    List<String> secondLevels = new ArrayList<>();

    Pattern p = Pattern.compile("(\\w+)\\.(\\w+)");

    for (var site: sites) {

        Matcher matcher = p.matcher(site);

        while (matcher.find()) {

            topLevels.add(matcher.group(1));
            secondLevels.add(matcher.group(2));
        }
    }

    System.out.println(topLevels);
    System.out.println(secondLevels);
}
```


## Stream pole

```java
import java.util.Arrays;

void main(String[] args)  {
    
    int[] vals = {-3, -2, 11, 2, 3, 4, 5, 0, -6, 7, 8, 9, 10};

    long len = Arrays.stream(vals).count();
    System.out.println(len);

    long suma = Arrays.stream(vals).sum();
    System.out.println(suma);

    long minVal = Arrays.stream(vals).min().getAsInt();
    System.out.println(minVal);

    long maxVal = Arrays.stream(vals).max().getAsInt();
    System.out.println(maxVal);
}
```



## Text na slova

```java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.List;
import java.util.regex.Pattern;

void main() throws IOException {

    Path myPath = Paths.get("src/resources/thermopylae.txt");
    String content = Files.readString(myPath, StandardCharsets.UTF_8);

    Pattern pattern = Pattern.compile("[\\s,.]+");
    List<String> words = pattern.splitAsStream(content).toList();

    System.out.println(words);
}
```


## Filtrovanie slov

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.List;
import java.util.stream.Stream;

void main() throws IOException {

    String fileName = "words.txt";

    Path path = Path.of(fileName);

    try (Stream<String> lines = Files.lines(path)) {

        List<String> words = lines.filter(word -> word.length() == 3).toList();

        words.forEach(System.out::println);
    }
}
```
