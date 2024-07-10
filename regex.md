# Regular expressions

Regular expressions are used for text searching and more advanced text  
manipulation. Regular expressions are built into tools including grep and Sed,  
text editors including vi and emacs, programming languages including Perl, Java,  
and C#.  

Java has built-in API for working with regular expressions; it is located in  
`java.util.regex`.


A regular expression defines a search pattern for strings. Pattern is a compiled  
representation of a regular expression. Matcher is an engine that interprets the  
pattern and performs match operations against an input string. Matcher has  
methods such as find, matches, end to perform matching operations. When there is  
an exception parsing a regular expression, Java throws a `PatternSyntaxException`.  

## Regex examples

The following table shows a couple of regular expression strings.  

| Regex | Meaning |
|-------|---------|
| . | Matches any single character. |
| ? | Matches the preceding element once or not at all. |
| + | Matches the preceding element once or more times. |
| * | Matches the preceding element zero or more times. |
| ^ | Matches the starting position within the string. |
| $ | Matches the ending position within the string. |
| \| | Alternation operator. |
| [abc] | Matches a or b, or c. |
| [a-c] | Range; matches a or b, or c. |
| [^abc] | Negation, matches everything except a, or b, or c. |
| \s | Matches white space character. |
| \w | Matches a word character; equivalent to [a-zA-Z_0-9] |

You can use this table in your markdown files to quickly reference regex symbols  
and their functions.  


## Simple regular expression

In the first example we match a word agains a list of words.  

```java
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    List<String> words = List.of("Seven", "even",
            "Maven", "Amen", "eleven");

    Pattern p = Pattern.compile(".even");

    for (String word: words) {

        Matcher m = p.matcher(word);

        if (m.matches()) {

            System.out.printf("%s matches%n", word);
        } else {

            System.out.printf("%s does not match%n", word);
        }
    }
}
```

In the example, we have five words in a list. We check which words match the  
`.even` regular expression.  

```java
Pattern p = Pattern.compile(".even");
```

We compile the pattern. The dot (.) metacharacter stands for any single  
character in the text.  

```java
for (String word: words) {

    Matcher m = p.matcher(word);

    if (m.matches()) {

        System.out.printf("%s matches%n", word);
    } else {

        System.out.printf("%s does not match%n", word);
    }
}
```

We go through the list of words. A matcher is created with the matcher method.  
The matches method returns true if the word matches the regular expression.  


## Regex word boundaries

The metacharacter `\b` is an anchor which matches at a position that is called a  
word boundary. It allows to search for whole words.  

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    var text = "This island is beautiful";

    Pattern p = Pattern.compile("\\bis\\b");
    Matcher matcher = p.matcher(text);

    while (matcher.find())
    {
        System.out.printf("%s at %d", matcher.group(), matcher.start());
    }
}
```

In the example, we look for the is word. We do not want to include the This and  
the island words.  

```java
Pattern p = Pattern.compile("\\bis\\b");
```

With two `\b` metacharacters, we search for the is whole word.

```java
while (matcher.find())
{
    System.out.printf("%s at %d", matcher.group(), matcher.start());
}
```

The `find` method attempts to find the next subsequence of the input sequence  
that matches the pattern. The group method returns the input subsequence matched  
by the previous match. The start method returns the start index of the previous  
match.  



## Implicit word boundaries

The `\w` is a character class used for a character allowed in a word. For the  
`\w+` regular expression, which denotes a word, the leading and trailing word  
boundary metacharacters are implicit; i.e. `\w+` is equal to `\b\w+\b`.  


```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    var content = """
Foxes are omnivorous mammals belonging to several genera
of the family Canidae. Foxes have a flattened skull, upright triangular ears,
a pointed, slightly upturned snout, and a long bushy tail. Foxes live on every
continent except Antarctica. By far the most common and widespread species of
fox is the red fox.""";

    Pattern p = Pattern.compile("\\w+");

    Matcher matcher = p.matcher(content);

    int count = 0;

    while (matcher.find()) {

        count++;
        System.out.println(matcher.group());
    }

    System.out.printf("There are %d words", count);
}
```

In the example, we search for all words in the text.  

```java
int count = 0;

while (matcher.find()) {

    count++;
    System.out.println(matcher.group());
}
```

We find all the words and count them.

## Regex currency symbol

The `\p{Sc}` regular expresion can be used to look for currency symbols.

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    String content = """
Currency symbols: ฿ Thailand bath, ₹ Indian rupee, ₾ Georgian lari, $ Dollar,
€ Euro, ¥ Yen, £ Pound Sterling""";

    String regex = "\\p{Sc}";

    Pattern pattern = Pattern.compile(regex, Pattern.CASE_INSENSITIVE);
    Matcher matcher = pattern.matcher(content);

    while (matcher.find())
    {
        System.out.printf("%s at %d%n", matcher.group(), matcher.start());
    }
}
```

In the example, we look for currency symbols.

```java
String content = """
    Currency symbols: ฿ Thailand bath, ₹ Indian rupee, ₾ Georgian lari, $ Dollar,
    € Euro, ¥ Yen, £ Pound Sterling""";
```

We have a couple of currency symbols in the text.

```java
String regex = "\\p{Sc}";
```

We define the regular expression for the currency symbols.  

```java
while (matcher.find())
{
    System.out.printf("%s at %d%n", matcher.group(), matcher.start());
}
```

We find all the symbols and their index.

```
฿ at 18
₹ at 35
₾ at 51
$ at 68
€ at 78
¥ at 86
£ at 93
```

## Regex anchors

Anchors match positions of characters inside a given text. In the next example,  
we look if a string is located at the beginning of a sentence.  

```java
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    List<String> sentences = List.of("I am looking for Jane.",
            "Jane was walking along the river.",
            "Kate and Jane are close friends.");

    Pattern p = Pattern.compile("^Jane");

    for (String word : sentences) {

        Matcher m = p.matcher(word);

        if (m.find()) {
            System.out.printf("%s matches%n", word);
        } else {
            System.out.printf("%s does not match%n", word);
        }
    }
}
```

We have three sentences. The search pattern is `^Jane`. The pattern checks if  
the "Jane" string is located at the beginning of the text. `Jane\.$` would look  
for "Jane" at the end of the sentence.  

## Regex alternations

The alternation operator `|` enables to create a regular expression with several  
choices.  

```java
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    List<String> users = List.of("Jane", "Thomas", "Robert",
            "Lucy", "Beky", "John", "Peter", "Andy");

    Pattern p = Pattern.compile("Jane|Beky|Robert");

    for (String user : users) {

        Matcher m = p.matcher(user);

        if (m.matches()) {
            System.out.printf("%s matches%n", user);
        } else {
            System.out.printf("%s does not match%n", user);
        }
    }
}
```

We have nine names in the list.

```java
Pattern p = Pattern.compile("Jane|Beky|Robert");
```

This regular expression looks for "Jane", "Beky", or "Robert" strings.

# Regex capturing groups

Round brackets are used to create capturing groups. This allows us to apply a  
quantifier to the entire group or to restrict alternation to a part of the  
regular expression.  

```java
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    var sites = List.of("webcode.me", "zetcode.com", "freebsd.org",
        "netbsd.org");

    Pattern p = Pattern.compile("(\\w+)\\.(\\w+)");

    for (var site: sites) {

        Matcher matcher = p.matcher(site);

        while (matcher.find()) {

            System.out.println(matcher.group(0));
            System.out.println(matcher.group(1));
            System.out.println(matcher.group(2));
        }

        System.out.println("*****************");
    }
}
```
In the example, we divide the domain names into two parts by using groups.

```java
Pattern p = Pattern.compile("(\\w+)\\.(\\w+)");
```

We define two groups with parentheses.

```java
while (matcher.find()) {

    System.out.println(matcher.group(0));
    System.out.println(matcher.group(1));
    System.out.println(matcher.group(2));
}
```

The groups are accessed via the group method. The `group(0)` returns the whole  
matched string.  

In the following example, we use groups to work with expressions.

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    String[] expressions = {"16 + 11", "12 * 5", "27 / 3", "2 - 8"};
    String pattern = "(\\d+)\\s+([-+*/])\\s+(\\d+)";

    for (var expression : expressions) {

        Pattern p = Pattern.compile(pattern);
        Matcher matcher = p.matcher(expression);

        while (matcher.find()) {

            int val1 = Integer.parseInt(matcher.group(1));
            int val2 = Integer.parseInt(matcher.group(3));
            String oper = matcher.group(2);

            var result = switch (oper) {

                case "+" -> String.format("%s = %d", expression, val1 + val2);
                case "-" -> String.format("%s = %d", expression, val1 - val2);
                case "*" -> String.format("%s = %d", expression, val1 * val2);
                case "/" -> String.format("%s = %d", expression, val1 / val2);
                default -> "Unknown operator";
            };

            System.out.println(result);
        }
    }
}
```

The example parses four simple mathematical expressions and computes them.  

```java
String[] expressions = {"16 + 11", "12 * 5", "27 / 3", "2 - 8"};
```

We have an array of four expressions.

```java
String pattern = "(\\d+)\\s+([-+*/])\\s+(\\d+)";
```

In the regex pattern, we have three groups: two groups for the values, one for  
the operator.  

```java
int val1 = Integer.parseInt(matcher.group(1));
int val2 = Integer.parseInt(matcher.group(3));
```

We get the values and transform them into integers.

```java
String oper = matcher.group(2);
```

We get the operator.

```java
var result = switch (oper) {

    case "+" -> String.format("%s = %d", expression, val1 + val2);
    case "-" -> String.format("%s = %d", expression, val1 - val2);
    case "*" -> String.format("%s = %d", expression, val1 * val2);
    case "/" -> String.format("%s = %d", expression, val1 / val2);
    default -> "Unknown operator";
};
```

With the switch expression, we compute the expressions.

## Count word frequency

In the next example, we count the frequency of words in a file.

```
$ wget https://raw.githubusercontent.com/janbodnar/data/main/the-king-james-bible.txt
```

We use the King James Bible.  

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.Collections;
import java.util.Map;
import java.util.function.Function;
import java.util.regex.MatchResult;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
import java.util.stream.Collectors;

void main() throws IOException {

    var fileName = "the-king-james-bible.txt";
    var text = Files.readString(Path.of(fileName));

    var regex = "[a-zA-Z']+";
    var p = Pattern.compile(regex);
    var matcher = p.matcher(text);

    var words = matcher.results();

    var res = words.collect(Collectors.groupingBy(MatchResult::group,
            Collectors.counting()));

    res.entrySet().stream()
            .sorted(Collections.reverseOrder(Map.Entry.comparingByValue()))
            .limit(10)
            .forEach((e -> System.out.printf("%s %d%n", e.getKey(), e.getValue())));
}
```

The results method returns a stream of matching results. We group the words by  
the number of times they are present. We sort them by the frequency and print  
the top ten words.  

```
the 62103
and 38848
of 34478
to 13400
And 12846
that 12576
in 12331
shall 9760
he 9665
unto 8942
```

## Replacing strings

It is possible to replace strings with `replaceAll` and `replaceFirst` methods.  
The methods return modified strings.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.URI;
import java.net.URL;
import java.nio.charset.StandardCharsets;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
import java.util.stream.Collectors;

void main() throws IOException {

    URL url = URI.create("https://webcode.me").toURL();

    try (InputStreamReader isr = new InputStreamReader(url.openStream(),
            StandardCharsets.UTF_8);
            BufferedReader br = new BufferedReader(isr)) {

        String content = br.lines().collect(
                Collectors.joining(System.lineSeparator()));

        Pattern p = Pattern.compile("<[^>]*>");

        Matcher matcher = p.matcher(content);
        String stripped = matcher.replaceAll("");

        System.out.println(stripped);
    }
}
```

The example reads HTML data of a web page and strips its HTML tags using a  
regular expression.  

```java
Pattern p = Pattern.compile("<[^>]*>");
```

This pattern defines a regular expression that matches HTML tags.  

```java
String stripped = matcher.replaceAll("");
```

We remove all the tags with replaceAll method.

## Splitting text

Text can be split with `Pattern's` `split` method.

```
22, 1, 3, 4, 5, 17, 18
2, 13, 4, 1, 8, 4
3, 21, 4, 5, 1, 48, 9, 42
```

We read from data.csv file.

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.List;
import java.util.regex.Pattern;

int sum = 0;

void main() throws IOException {

    Path myPath = Paths.get("data.csv");
    List<String> lines = Files.readAllLines(myPath);

    String regex = ",";
    Pattern p = Pattern.compile(regex);

    lines.forEach((line) -> {

        String[] parts = p.split(line);

        for (String part : parts) {

            String val = part.trim();

            sum += Integer.parseInt(val);
        }

    });

    System.out.printf("Sum of values: %d", sum);
}
```

The examples reads values from a CSV file and computes the sum of them. It uses  
regular expression to read the data.  

```java
List<String> lines = Files.readAllLines(myPath);
```

In one shot, we read all data into the list of strings with `Files.readAllLines`.

```java
String regex = ",";
```

The regular expression is a comma character.

```java
lines.forEach((line) -> {

    String[] parts = p.split(line);

    for (String part : parts) {

        String val = part.trim();

        sum += Integer.parseInt(val);
    }

});
```

We go through the lines and split them into an array of strings with `split`. We  
cut off spaces with trim and compute the sum value.  

# Case-insensitive regular expression

By setting the `Pattern.CASE_INSENSITIVE` flag, we can have case-insensitive  
matching.  


```java
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    List<String> users = List.of("dog", "Dog", "DOG", "Doggy");
    Pattern p = Pattern.compile("dog", Pattern.CASE_INSENSITIVE);

    users.forEach((user) -> {

        Matcher m = p.matcher(user);

        if (m.matches()) {
            System.out.printf("%s matches%n", user);
        } else {
            System.out.printf("%s does not match%n", user);
        }
    });
}
```

The example performs case-insensitive matching of the regular expression.

```java
Pattern p = Pattern.compile("dog", Pattern.CASE_INSENSITIVE);
```

Case-insensitive matching is set by setting `Pattern.CASE_INSENSITIVE` as the  
second parameter to `Pattern.compile`.  

## Subpatterns

Subpatterns are patterns within patterns. Subpatterns are created with `()`  
characters.  

```java
import java.util.Arrays;
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    List<String> words = Arrays.asList("book", "bookshelf", "bookworm",
            "bookcase", "bookish", "bookkeeper", "booklet", "bookmark");

    Pattern p = Pattern.compile("book(worm|mark|keeper)?");

    for (String word : words) {

        Matcher m = p.matcher(word);

        if (m.matches()) {
            System.out.printf("%s matches%n", word);
        } else {
            System.out.printf("%s does not match%n", word);
        }
    }
}
```

The example creates a subpattern.

```java
Pattern p = Pattern.compile("book(worm|mark|keeper)?");
```

The regular expression uses a subpattern. It matches bookworm, bookmark,  
bookkeeper, and book words.

## Email example

In the following example, we create a regex pattern for checking email addresses.  

```java
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    List<String> emails = List.of("luke@gmail.com",
            "andy@yahoocom", "34234sdfa#2345", "f344@gmail.com");

    String regex = "[a-zA-Z0-9._-]+@[a-zA-Z0-9-]+\\.[a-zA-Z.]{2,18}";

    Pattern p = Pattern.compile(regex);

    for (String email : emails) {

        Matcher m = p.matcher(email);

        if (m.matches()) {
            System.out.printf("%s matches%n", email);
        } else {
            System.out.printf("%s does not match%n", email);
        }
    }
}
```

This example provides only one possible solution.

```java
String regex = "[a-zA-Z0-9._-]+@[a-zA-Z0-9-]+\\.[a-zA-Z.]{2,18}";
```

The email is divided into five parts. The first part is the local part. This is  
usually a name of a company, individual, or a nickname. The `[a-zA-Z0-9._-]+`  
lists all possible characters, we can use in the local part. They can be used  
one or more times.  

The second part consists of the literal `@` character. The third part is the  
domain part. It is usually the domain name of the email provider, like yahoo, or  
gmail. The `[a-zA-Z0-9-]+` is a character set providing all characters that can  
be used in the domain name. The + quantifier makes use of one or more of these  
characters.

The fourth part is the dot character. It is preceded by the escape character  
`(\)`. This is because the dot character is a metacharacter and has a special  
meaning. By escaping it, we get a literal dot.  

The final part is the top level domain: `[a-zA-Z.]{2,18}`. Top level domains can  
have from 2 to 18 characters, such as sk, net, info, travel, cleaning,  
travelinsurance. The maximum length can be 63 characters, but most domain are  
shorter than 18 characters today. There is also a dot character. This is because  
some top level domains have two parts; for example `co.uk`.  
