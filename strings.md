# Strings

We work with strings in Java using `String` and `StringBuilder`.

## Definition

In Java, a string is a sequence of Unicode characters. Strings are objects.  
There are two basic classes for working with strings:

- `String`
- `StringBuilder` 

`String` is an immutable sequence of characters. `StringBuilder` is a mutable  
sequence of characters. (There is also a StringBuffer class which can be used by  
multiple threads. If we are not dealing with threads, we use the StringBuilder.)  

A string literal a series of characters in the source code that is enclosed in  
double quotes. For example, "Java" is a string literal. Whenever Java compiler  
encounters a string literal in the code, it creates a String object with its  
value.  

```java
String lang = "Java"; // same as String lang = new String("Java");
```

String literals are used by many programming languages. It is an established  
convention and it also saves typing.  

# Initializing strings

There are multiple ways of creating strings, both immutable and mutable.  
We will show a few of them.

```java
void main() {

    char[] cdb = {'M', 'y', 'S', 'Q', 'L'};

    String lang = "Java";
    String ide = new String("NetBeans");
    String db = new String(cdb);

    System.out.println(lang);
    System.out.println(ide);
    System.out.println(db);

    StringBuilder sb1 = new StringBuilder(lang);
    StringBuilder sb2 = new StringBuilder();
    sb2.append("Fields");
    sb2.append(" of ");
    sb2.append("glory");

    System.out.println(sb1);
    System.out.println(sb2);
}
```

The example shows a few ways of creating `String` and `StringBuilder` objects.

```java
String lang = "Java";
```

The most common way is to create a string object from a string literal.

```java
String ide = new String("NetBeans");
```

In this line, we create a string using the usual way of building objects — with
the `new` keyword.  

```java
String db = new String(cdb);
```

Here we create a string object from an array of characters.

```java
StringBuilder sb1 = new StringBuilder(lang);
```

A `StringBuilder` object is created from a `String`.

```java
StringBuilder sb2 = new StringBuilder();
sb2.append("Fields");
sb2.append(" of ");
sb2.append("glory");
```

We create an empty `StringBuilder` object. We append three strings into the object.  


## A string is an object

Strings are objects; they are not primitive data types. Strings are instances of  
the `String` or `StringBuilder` class. Since they are objects, they have  
multiple methods available for doing various work.  

```java
void main() {

    String lang = "Java";

    String bclass = lang.getClass().toString();
    System.out.println(bclass);

    String sup = lang.getClass().getSuperclass().toString();
    System.out.println(sup);

    if (lang.isEmpty()) {

        System.out.println("The string is empty");
    } else {

        System.out.println("The string is not empty");
    }

    int l = lang.length();
    System.out.println("The string has " + l + " characters");
}
```

In this program, we demonstrate that strings are objects. Objects must have a  
class name, a parent class, and they must also have some methods that we can  
call.

```java
String lang = "Java";
```

An object of `String` type is created.

```java
String bclass = lang.getClass().toString();
```

We determine the class name of the object to which the lang variable refers.

```java
String sup = lang.getClass().getSuperclass().toString();
```

A parent class of our object is received. All objects have at least one parent —
the Object.

```java
if (lang.isEmpty()) {

    System.out.println("The string is empty");
} else {

    System.out.println("The string is not empty");
}
```

Objects have various methods. One of the useful string methods is the `isEmpty`  
method, which determines whether the string is empty.  

```java
int l = lang.length();
```

The length method returns the size of the string.


##  String length

It is not easy to determine the length of a Unicode string. The `length` method  
works only for certain Unicode characters.  

```java
void main() {

    var text1 = "falcon";
    var n1 = text1.length();

    System.out.printf("%s has %d characters%n", text1, n1);

    System.out.println("----------------------------");

    var text2 = "вишня";
    var n2 = text2.length();
    System.out.printf("%s has %d characters%n", text2, n2);

    System.out.println("----------------------------");

    var text3 = "🐺🦊🦝";
    var n3 = text3.length();
    System.out.printf("%s has %d characters%n", text3, n3);

    var n3_ = graphemeLength(text3);
    System.out.printf("%s has %d characters%n", text3, n3_);

    System.out.println("----------------------------");

    var text4 = "नमस्ते";

    var n4 = text4.length();
    System.out.printf("%s has %d characters%n", text4, n4);

    var n4_ = graphemeLength(text4);
    System.out.printf("%s has %d characters%n", text4, n4_);
}

int graphemeLength(String text) {

    BreakIterator it = BreakIterator.getCharacterInstance();
    it.setText(text);

    int count = 0;

    while (it.next() != BreakIterator.DONE) {
        count++;
    }

    return count;
}
```

In the example, we try to determine the length of various text.

```java
var text1 = "falcon";
var n1 = text1.length();
```

For basic latin characters, the `length` method works OK.  

```java
var text2 = "вишня";
var n2 = text2.length();
```

It also works OK for this cyrillic text.

```java
var text3 = "🐺🦊🦝";
var n3 = text3.length();
```

For emojis, we get a wrong result with length.  

```java
var n3_ = graphemeLength(text3);
```

With `BreakIterator` used in graphemeLength, we get the correct result for emojis.  

```java
var text4 = "नमस्ते";

var n4 = text4.length();
System.out.printf("%s has %d characters%n", text4, n4);

var n4_ = graphemeLength(text4);
System.out.printf("%s has %d characters%n", text4, n4_);
```

However for sanskrit, both methods return a wrong result. (The correct answer  
is four characters.)


## Mutable & immutable strings

The `String` is a sequence of immutable characters, while the `StringBuilder` is  
a sequence of mutable characters. The next example will show the difference.  

```java
void main() {

    String name = "Jane";
    String name2 = name.replace('J', 'K');
    String name3 = name2.replace('n', 't');

    System.out.println(name);
    System.out.println(name3);

    StringBuilder sb = new StringBuilder("Jane");
    System.out.println(sb);

    sb.setCharAt(0, 'K');
    sb.setCharAt(2, 't');

    System.out.println(sb);
}
```

Both objects have methods for replacing characters in a string.

```java
String name = "Jane";
String name2 = name.replace('J', 'K');
String name3 = name2.replace('n', 't');
```

Calling the replace method on a `String` results in returning a new modified   
string. The original string is not changed.  

```java
sb.setCharAt(0, 'K');
sb.setCharAt(2, 't');
```

The `setCharAt` method of a StringBuilder will replace a character at the given  
index with a new character. The original string is modified.


## The isBlank method

The `isBlank` method returns true if the string is empty or contains only white
space.

```java
import java.util.List;

void main() {

    var data = List.of("sky", "\n\n", "  ", "blue", "\t\t", "", "sky");

    for (int i = 0; i < data.size(); i++) {

        var e = data.get(i);

        if (e.isBlank()) {

            System.out.printf("element with index %d is blank%n", i);
        } else {

            System.out.println(data.get(i));
        }
    }
}
```

We go through a list of strings and print all blank elements.  


## Concatenating strings

Immutable strings can be added using the `+` operator or the concat method. They  
will form a new string which is a chain of all concatenated strings. Mutable  
strings have the append method which builds a string from any number of other  
strings.  


```java
void main() {

    System.out.println("Return" + " of " + "the king.");
    System.out.println("Return".concat(" of ").concat("the king."));

    StringBuilder sb = new StringBuilder();
    sb.append("Return");
    sb.append(" of ");
    sb.append("the king.");

    System.out.println(sb);
}
```

The example creates three sentences by adding strings.

```java
System.out.println("Return" + " of " + "the king.");
```

A new string is formed by using the `+` operator.

```java
System.out.println("Return".concat(" of ").concat("the king."));
```

The `concat` method returns a string that represents the concatenation of this  
object's characters followed by the string argument's characters.  

```java
StringBuilder sb = new StringBuilder();
sb.append("Return");
sb.append(" of ");
sb.append("the king.");
```

A mutable object of the `StringBuilder` type is created by calling the `append`
method three times.

## Using quotes

In certain cases, such as using direct speech, the inner quotes must be escaped.

```java
    void main() {

        System.out.println("There are may stars");
        System.out.println("He said: \"Which one are you looking at?\"");
    }
}
```

We use the `\` character to escape additional quotes.

## Multiline strings

Text blocks allow to define multi-line strings. To create a multi-line string,
we use triple quotes.

```java
String lyrics = """
    I cheated myself
    like I knew I would
    I told ya, I was trouble
    you know that I'm no good""";


void main() {

    System.out.println(lyrics);
}
```

We have a strophe that spans four lines.


Before text blocks were introduced, we had to do a concatenation operation and  
use the `\n` character.  

```java
String lyrics = "I cheated myself\n" +
    "like I knew I would\n" +
    "I told ya, I was trouble\n" +
    "you know that I'm no good";


void main() {

    System.out.println(lyrics);
}
```

The four strings are concatenated with the `+` operator.  

## String elements

A string is a sequence of characters. A character is a basic element of a  
string. The following two examples show some methods that work with characters  
of a string.  

```java
void main() {

    char[] crs = {'Z', 'e', 't', 'C', 'o', 'd', 'e' };
    String s = new String(crs);

    char c1 = s.charAt(0);
    char c2 = s.charAt(s.length()-1);

    System.out.println(c1);
    System.out.println(c2);

    int i1 = s.indexOf('e');
    int i2 = s.lastIndexOf('e');

    System.out.println("The first index of character e is " + i1);
    System.out.println("The last index of character e is " + i2);

    System.out.println(s.contains("t"));
    System.out.println(s.contains("f"));

    char[] elements = s.toCharArray();

    for (char el : elements) {

        System.out.println(el);
    }
}
```

In the first example, we will work with an immutable string.  
 
```java
char[] crs = {'Z', 'e', 't', 'C', 'o', 'd', 'e' };
String s = new String(crs);
```

A new immutable string is formed from an array of characters.  

```java
char c1 = s.charAt(0);
char c2 = s.charAt(s.length()-1);
```

With the `charAt` method, we get the first and the last char value of the string.  

```java
int i1 = s.indexOf('e');
int i2 = s.lastIndexOf('e');
```

With the `indexOf` and `lastIndexOf` methods, we get the first and the last  
occurrence of the character 'e'.  

```java
System.out.println(s.contains("t"));
```

With the `contains` method, we check if the string contains the t character. The  
method returns a boolean value.  

```java
char[] elements = s.toCharArray();

for (char el : elements) {

    System.out.println(el);
}
```

The `toCharArray` method creates a character array from the string. We go  
through the array and print each of the characters.  


In the second example, we work with the elements of a `StringBuilder` class.  


```java
void main() {
    StringBuilder sb = new StringBuilder("Misty mountains");
    System.out.println(sb);

    sb.deleteCharAt(sb.length()-1);
    System.out.println(sb);

    sb.append('s');
    System.out.println(sb);

    sb.insert(0, 'T');
    sb.insert(1, 'h');
    sb.insert(2, 'e');
    sb.insert(3, ' ');
    System.out.println(sb);

    sb.setCharAt(4, 'm');
    System.out.println(sb);
}
```

A mutable string is formed. We modify the contents of the string by deleting,  
appending, inserting, and replacing characters.  

```java
sb.deleteCharAt(sb.length()-1);
```

This line deletes the last character.

```java
sb.append('s');
```

The deleted character is appended back to the string.

```java
sb.insert(0, 'T');
sb.insert(1, 'h');
sb.insert(2, 'e');
sb.insert(3, ' ');
```

We insert four characters at the beginning of the string.

```java
sb.setCharAt(4, 'm');
```

Finally, we replace a character at index 4.  


## String repeat

The `repeat` method returns a string that is repeated n times.  

```java
void main() {

    var word = "falcon ";

    var output = word.repeat((5));
    System.out.println(output);
}
```

In the example, we repeat the word five times.  


##  String lines

The lines method returns a stream of lines extracted from the string, separated  
by line terminators.  

```java
void main() {

    var words = """
            club
            sky
            blue
            cup
            coin
            new
            cent
            owl
            falcon
            brave
            war
            ice
            paint
            water
            """;

    var wstream = words.lines();

    wstream.forEach(word -> {

        if (word.length() == 3) {
            System.out.println(word);
        }
    });
}
```

We have fourteen words in the text block.  

```java
var wstream = words.lines();
```

With the lines method we create a stream of these words.  

```java
wstream.forEach(word -> {

    if (word.length() == 3) {
        System.out.println(word);
    }
});
```

We go over the stream with `forEach` and print all words having length of three  
letters.  


## The startsWith method

The `startsWith` checks if the string starts with the given prefix.

```java
void main(String[] args) {

    var words = "club\nsky\nblue\ncup\ncoin\nnew\ncent\nowl\nfalcon\nwar\nice";

    var wstream = words.lines();
    wstream.forEach(word -> {

        if (word.startsWith("c")) {
            System.out.println(word);
        }
    });
}
```

We have a couple of words in a string. We print all words that start with letter
c.

## The endsWith method 

The `endsWith` method checks if the string ends with the specified suffix.

```java
void main(String[] args) {

    var words = "club\nsky\nblue\ncup\ncoin\nnew\ncent\nowl\nfalcon\nwar\nice";

    var wstream = words.lines();
    wstream.forEach(word -> {

        if (word.endsWith("n") || word.endsWith("y")) {
            System.out.println(word);
        }
    });
}
```

In the example, we print all words that end either with n or y.  


## The toUpperCase/toLowerCase methods

The `toUpperCase` method converts all of the characters of the string to upper  
case. The toLowerCase method converts all of the characters of the string to  
lower case.

```java
 void main() {

    var word1 = "Cherry";

    var u_word1 = word1.toUpperCase();
    var l_word1 = u_word1.toLowerCase();

    System.out.println(u_word1);
    System.out.println(l_word1);

    var word2 = "Čerešňa";

    var u_word2 = word2.toUpperCase();
    var l_word2 = u_word2.toLowerCase();

    System.out.println(u_word2);
    System.out.println(l_word2);
}
```

We modify the case of two words.


## The matches method

The `matches` method tells whether or not the string matches the given regular  
expression.  

```java
void main() {

    var words = """
            book
            bookshelf
            bookworm
            bookcase
            bookish
            bookkeeper
            booklet
            bookmark
            """;

    var wstream = words.lines();

    wstream.forEach(word -> {
        if (word.matches("book(worm|mark|keeper)?")) {
            System.out.println(word);
        }
    });
}
```

In the example, we print all the words that satisfy the specified subpatterns.

## Palindrome

A palindrome is a word, number, phrase, or other sequence of characters which  
reads the same backward as forward, such as madam or racecar. There are many  
ways to check if a string is a palindrome. The following example is one of the  
possible solutions.  

```java
// A palindrome is a word, number, phrase, or other sequence of characters
// which reads the same backward as forward, such as madam or racecar

void main() {

        System.out.println(isPalindrome("radar"));
        System.out.println(isPalindrome("kayak"));
        System.out.println(isPalindrome("forest"));
}

boolean isPalindrome(String original) {

    char[] data = original.toCharArray();

    int i = 0;
    int j = data.length - 1;

    while (j > i) {

        if (data[i] != data[j]) {
            return false;
        }

        ++i;
        --j;
    }

    return true;
}
```

We have an implementation of the `isPalindrome` method.  

```java
boolean isPalindrome(String original) {

    char[] data = original.toCharArray();
...
```

We turn the string into a array of characters.  

```java
int i = 0;
int j = data.length - 1;

while (j > i) {

    if (data[i] != data[j]) {
        return false;
    }

    ++i;
    --j;
}

return true;
```

We iterate through the array and compare the left side characters with the right  
side corresponding characters. If all match, we return true, otherwise we return  
false.


## Substrings

The `substring` method returns a part of a string. The beginning index is  
inclusive, the ending index is exclusive. The beginning index starts from zero.  

```java
void main() {

    String str = "bookcase";

    System.out.println(str.substring(0, 4));
    System.out.println(str.substring(4, str.length()));
}
```

The example uses the `substring` method to create two substrings.

```java
System.out.println(str.substring(0, 4));
```

Here we get the "book" substring. The zero refers to the first character of the  
string.  

```java
System.out.println(str.substring(4, str.length()));
```

Here the "case" substring is printed.

## The split method

The `split` method cuts a string into parts; it takes a delimiting regular
expression as a parameter.

```java
void main() {

    String s = "Today is a beautiful day.";

    String[] words = s.split(" ");

    for (String word : words) {

        System.out.println(word);
    }
}
```

The example splits a sentence into words.

```java
String s = "Today is a beautiful day.";
```

This is a sentence to be split. The words are separated by a space character.  

```java
String[] words = s.split(" ");
```

Using the `split` method, we cut the sentence into words. The space character is  
used as a delimiter. The method returns an array of strings.  

```java
for (String word : words) {

    System.out.println(word);
}
```

We go throught the array and print its content.


## Removing string characters

When we split a string into words, some words have starting or ending characters  
such as comma or dot. In the next example, we show how to remove such  
characters.  

```java
void main(String[] args) {

    String str = "Did you go there? We did, but we had a \"great\" service there.";

    String[] parts = str.split(" ");

    for (String part: parts) {

        String word = removeChars(part);
        System.out.println(word);
    }
}

String removeChars(String part) {

    String word = part;

    if (part.endsWith(".") || part.endsWith("?") || part.endsWith(",")
            || part.endsWith("\"")) {
        word = part.substring(0, part.length()-1);
    }

    if (part.startsWith("\"")) {
        word = word.substring(1, part.length()-1);
    }

    return word;
}
```

The example split a string into words and removes potential commas, dots,  
question marks, or double quotation marks.  

String str = "Did you go there? We did, but we had a \"great\" service there.";  
In this string, we have a question mark, a comma, quotation marks, and a dot  
attached to the words.  

```java
private static String removeChars(String part) {
```

Inside this custom method, we remove those characters from our words.

```java
if (part.endsWith(".") || part.endsWith("?") || part.endsWith(",")
    || part.endsWith("\"")) {
    word = part.substring(0, part.length()-1);
}
```

In this if statement, we remove the ending character. We use the endsWith method  
to identify the characters that we want to remove. The substring method returns  
a part of the string without the character.  

```java
if (part.startsWith("\"")) {
    word = word.substring(1, part.length()-1);
}
```

Also, we remove the starting characters. The starting character is checked with  
the startsWith method.  

## Joining strings

There is a join method to join strings. Refer to Java `StringJoiner` to learn  
more about joining strings in Java.  

```java
void main() {

    String joined = String.join(" ", "Today", "is", "Sunday");
    System.out.println(joined);
}
```

In the example, we joing three strings into one final string.  

```java
String joined = String.join(" ", "Today", "is", "Sunday");
```

The first parameter of the join method is a delimiter that is going to separater  
each string in the final string. The rest of the parameters are strings to be  
joined.  

## Comparing strings

There are two basic methods for comparing strings. The `equals` method compares  
the contents of two strings and returns a boolean value indicating, whether the  
strings are equal or not. The `equalsIgnoreCase` does the same thing, except  
that it ignores the case.

```java
void main() {

    String a = "book";
    String b = "Book";

    System.out.println(a.equals(b));
    System.out.println(a.equalsIgnoreCase(b));
}
```

We compare two strings using the aforementioned methods.

```java
String a = "book";
String b = "Book";
```

We define two strings that we compare.

```java
System.out.println(a.equals(b));
```

The equals method returns `false`. The two strings differ in the first character.  

```java
System.out.println(a.equalsIgnoreCase(b));
```

When we ignore the case, the strings are equal: the `equalsIgnoreCase` method  
returns `true`.

If we are comparing a variable to a string, it is important to remember that the  
string should be on the left side of the comparing method. Otherwise we might  
get a `NullPointerException`.  

```java
import java.util.Random;

String readString() {

    Random r = new Random();
    boolean b = r.nextBoolean();

    if (b == true) {

        return "ZetCode";
    } else {

        return null;
    }
}

void main() {

    String d = readString();

    if ("ZetCode".equals(d)) {

        System.out.println("Strings are equal");
    } else {

        System.out.println("Strings are not equal");
    }
}
```

In the code example, we compare the strings properly, avoiding a possible  
`NullPointerException`.

```java
String readString() {

    Random r = new Random();
    boolean b = r.nextBoolean();

    if (b == true) {

        return "ZetCode";
    } else {

        return null;
    }
}
```

The `readString` method simulates the case where a method invocation can result  
in a `null` value. This could happen, for instance, if we try to read a value  
from a database.  

```java
String d = readString();
```

The `d` variable can contain the `null` value.

```java
if ("ZetCode".equals(d)) {
```

The above line is the correct way of comparing two strings where one string is a  
known literal. If we placed the d variable on the left side, this would lead to  
`NullPointerException` if the d variable would contain the null value.  

The equals method compares the characters of two strings. The `==` operator  
tests for reference equality. All string literals are interned automatically in  
Java. They are placed inside a string pool. This happens at compile time. If two  
variables contain two equal string literals, they in fact refer to the same  
string object inside a string pool.  

```java
void main() {

    boolean a = "ZetCode" == "ZetCode";
    boolean b = "ZetCode" == new String("ZetCode");
    boolean c = "ZetCode" == "Zet" + "Code";
    boolean d = "ZetCode" == new String("ZetCode").intern();
    boolean e = "ZetCode" == " ZetCode ".trim();

    System.out.println(a);
    System.out.println(b);
    System.out.println(c);
    System.out.println(d);
    System.out.println(e);
}
```

In this code example, we compare string objects with the `==` operator.  

```java
boolean a = "ZetCode" == "ZetCode";
```

These strings literals are interned. Therefore, the identity comparison operator  
returns true.

```java
boolean b = "ZetCode" == new String("ZetCode");
```

Strings created with the new operator are not interned. The comparison operator  
results in a `false` value.  

```java
boolean c = "ZetCode" == "Zet" + "Code";
```

Strings are concatenated at compile time. The string literals result in the same  
object. The result is a `true`.  

```java
boolean d = "ZetCode" == new String("ZetCode").intern();
```

The `intern` object puts the string object on the right side into the pool.  
Therefore, the `d` variable holds a boolean `true`.  

```java
boolean e = "ZetCode" == " ZetCode ".trim();
```

The `trim` method is called at runtime, generating a distinct object. The `e`
variable holds a boolean `false`.



## Format string

We have three basic methods to format a string in Java. Refer to Java String  
format for a more details.  

```java
void main() {

    String name = "John Doe";
    String occupation = "gardener";

    String txt = "%s is a %s";
    String msg = txt.formatted(name, occupation);

    System.out.println(msg);

    System.out.format("%s is a %s\n", name, occupation);
    System.out.printf("%s is a %s%n", name, occupation);
}
```

We build the same string three times.  

```java
String name = "John Doe";
String occupation = "gardener";

String txt = "%s is a %s";
String msg = txt.formatted(name, occupation);
```

The `formatted` method is an instance method. The `%s` is a string format  
specifier, which is replaced with an actual value.  

```java
System.out.format("%s is a %s\n", name, occupation);
System.out.printf("%s is a %s%n", name, occupation);
```

The `format` and `printf` methods are static.  
