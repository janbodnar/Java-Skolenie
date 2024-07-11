# JSoup

JSoup is a Java library for extracting and manipulating HTML data. It implements  
the HTML5 specification, and parses HTML to the same DOM as modern browsers.  

## JSoup features

- scrape and parse HTML from a URL, file, or string
- find and extract data, using DOM traversal or CSS selectors
- manipulate the HTML elements, attributes, and text
- clean user-submitted content against a safe white-list, to prevent XSS attacks
- output tidy HTML

## Dependency

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

## JSoup class

`JSoup` class provides the core public access point to the jsoup functionality  
via its static methods. For instance, the clean methods sanitize HTML code, the  
connect method creates a connection to URL, or parse methods parse HTML content.  

## HTML file
In some of the examples, we use the following `words.html` file:  

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document title</title>
</head>
<body>
<p>List of words</p>
<ul>
    <li>dark</li>
    <li>smart</li>
    <li>war</li>
    <li>cloud</li>
    <li>park</li>
    <li>cup</li>
    <li>worm</li>
    <li>water</li>
    <li>rock</li>
    <li>warm</li>
</ul>
<footer>footer for words</footer>
</body>
</html>
```

## Parse HTML string

The `JSoup.parse` method perses an HTML string into a document.

```java
package com.zetcode;

import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class JSoupFromStringEx {

    public static void main(String[] args) {

        String htmlString = """
                <html><head><title>My title</title></head>
                <body>Body content</body></html>""";

        Document doc = Jsoup.parse(htmlString);
        String title = doc.title();
        String body = doc.body().text();

        System.out.printf("Title: %s%n", title);
        System.out.printf("Body: %s", body);
    }
}
```

The example parses a HTML string and outputs its title and body content.  

```java
String htmlString = """
    <html><head><title>My title</title></head>
    <body>Body content</body></html>""";
```

This string contains simple HTML data.  

```java
Document doc = Jsoup.parse(htmlString);
```

With the Jsoup's parse method, we parse the HTML string. The method returns a  
HTML document.  

```java
String title = doc.title();
```

The document's title method gets the string contents of the document's title  
element.  

```java
String body = doc.body().text();
```

The document's body method returns the body element; its text method gets the  
text of the element.  

## Parse local HTML file

In the second example, we are going to parse a local HTML file. We use the  
overloaded `Jsoup.parse` method that takes a File object as its first parameter.  

```html
<!DOCTYPE html>
<html>
    <head>
        <title>My title</title>
        <meta charset="UTF-8">
    </head>
    <body>
        <div id="mydiv">Contents of a div element</div>
    </body>
</html>
```

For the example, we use the above HTML file.  

```java
package com.zetcode;

import java.io.File;
import java.io.IOException;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;

public class JSoupFromFileEx {
    
    public static void main(String[] args) throws IOException {
        
        String fileName = "src/main/resources/index.html";
        
        Document doc = Jsoup.parse(new File(fileName), "utf-8"); 
        Element divTag = doc.getElementById("mydiv"); 
        
        System.out.println(divTag.text());
    }
}
```

The example parses the `index.html` file, which is located in the  
`src/main/resources/` directory.  

```java
Document doc = Jsoup.parse(new File(fileName), "utf-8"); 
```

We parse the HTML file with the `Jsoup.parse` method.  

```java
Element divTag = doc.getElementById("mydiv"); 
```

With the document's `getElementById` method, we get the element by its ID.  

```java
System.out.println(divTag.text());
```

The text of the tag is retrieved with the element's `text` method.  

## Read web site's title

In the following example, we scrape and parse a web page and retrieve the  
content of the `title` element.  

```java
package com.zetcode;

import java.io.IOException;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class JSoupTitleEx {

    public static void main(String[] args) throws IOException {
        
        String url = "https://webcode.me";
        
        Document doc = Jsoup.connect(url).get();
        String title = doc.title();
        System.out.println(title);
    }
}
```

In the code example, we read the title of a specified web page.  

```java
Document doc = Jsoup.connect(url).get();
```

The Jsoup's connect method creates a connection to the given URL. The get method  
executes a GET request and parses the result; it returns a HTML document.  

```java
String title = doc.title();
```

With the document's `title` method, we get the title of the HTML document.  

## Read web page

The next example retrieves the HTML source of a web page.  

```java
package com.zetcode;

import java.io.IOException;
import org.jsoup.Jsoup;

public class JSoupHtmlPageEx {

    public static void main(String[] args) throws IOException {

        String webPage = "http://webcode.me";
        String html = Jsoup.connect(webPage).get().html();

        System.out.println(html);
    }
}
```

The example prints the HTML of a web page.

```java
String html = Jsoup.connect(webPage).get().html();
```

The `html` method returns the HTML of an element; in our case the HTML source of  
the whole document.  

## JSoup get information

Meta information of a HTML document provides structured metadata about a Web  
page, such as its description and keywords.  

```java
package com.zetcode;

import java.io.IOException;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class JSoupMetaInfoEx {

    public static void main(String[] args) throws IOException {

        String url = "https://jsoup.org";
        Document document = Jsoup.connect(url).get();

        String description = document.select("meta[name=description]")
                .first().attr("content");
        System.out.println("Description : " + description);

        String keywords = document.select("meta[name=keywords]")
                .first().attr("content");
        System.out.println("Keywords : " + keywords);
    }
}
```

The code example retrieves meta information about a specified web page.  

```java
String keywords = document.select("meta[name=keywords]")
    .first().attr("content");
```

The document's `select` method finds elements that match the given query. The  
first method returns the first matched element. With the `attr` method, we get  
the value of the content attribute.  

## Get all tags
 
To get all tags, we pass the `*` character to the `select` method. 

```java
package com.zetcode;

import org.jsoup.Jsoup;

import java.io.File;
import java.io.IOException;

public class JSoupAll {

    public static void main(String[] args) throws IOException {

        var fileName = "src/main/resources/words.html";
        var myFile = new File(fileName);

        var doc = Jsoup.parse(myFile, "UTF-8");
        var all = doc.body().select("*");

        all.forEach(e -> System.out.println(e.tagName()));
    }
}
```

We get all the tags from the words.html document.  

```java
var all = doc.body().select("*");
```

We get all elements.  

```java
all.forEach(e -> System.out.println(e.tagName()));
```

We go over all the elements and print their tag names with tagName.  

## JSoup text

The `text` method gets the combined text of this element and all its children.  
The whitespace is normalized and trimmed.  

```java
package com.zetcode;

import org.jsoup.Jsoup;

import java.io.File;
import java.io.IOException;

public class JSoupGetText {

    public static void main(String[] args) throws IOException {

        var fileName = "src/main/resources/words.html";
        var myFile = new File(fileName);

        var doc = Jsoup.parse(myFile, "UTF-8");

        System.out.println(doc.text());

        System.out.println("---------------------------");
        System.out.println(doc.body().text());

        System.out.println("---------------------------");
        var e1 = doc.select("body>p").first();
        System.out.println(e1.text());

        System.out.println("---------------------------");
        var e2 = doc.select("body>ul").first();
        System.out.println(e2.text());

        System.out.println("---------------------------");
        var lis = e2.children();
        System.out.println(lis.first().text());
        System.out.println(lis.last().text());
    }
}
```

In the example, we get the text data from the whole document, body, paragraph,  
unordered list, and first and last list item.  


## Change text

The overloaded text method sets the text of the specified element.

```java
package com.zetcode;

import org.jsoup.Jsoup;

public class JSoupChangeText {

    public static void main(String[] args) {

        String htmlString = """
                <html><head><title>My title</title></head>
                <body>Body content</body></html>""";

        var doc = Jsoup.parse(htmlString);
        doc.body().text("Lorem ipsum dolor sit amet");

        System.out.println(doc);
    }
}
```

In the example, we change the text inside the body tag.  

## Modify document

There are multiple methods for modifying the HTML document. For instance, the  
append method appends a tag and the prepend method prepends a tag to an element.  

```java
package com.zetcode;

import org.jsoup.Jsoup;

public class JSoupModify {

    public static void main(String[] args) {

        String htmlString = """
                <html><head><title>My title</title></head>
                <body></body></html>""";

        var doc = Jsoup.parse(htmlString);

        var e = doc.select("body").first();
        e.append("<p>hello there!</p>");
        e.prepend("<h1>Heading</h1>");
        
        System.out.println(doc);
    }
}
```
In the example, we add `h1` and `p` tags to the document.  


## Parse links

The next example parses links from a HTML page.

```java
package com.zetcode;

import java.io.IOException;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

public class JSoupLinksEx {

    public static void main(String[] args) throws IOException {
        
        String url = "https://jsoup.org";

        Document document = Jsoup.connect(url).get();
        Elements links = document.select("a[href]");
        
        for (Element link : links) {
            
            System.out.println("link : " + link.attr("href"));
            System.out.println("text : " + link.text());
        }
    }
}
```

In the example, we connect to a web page and parse all its link elements.  

```java
Elements links = document.select("a[href]");
```

To get a list of links, we use the document's `select` method.

## Sanitize HTML data

JSoup provides methods for sanitizing HTML data.

```java
package com.zetcode;

import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.safety.Cleaner;
import org.jsoup.safety.Whitelist;

public class JSoupSanitizeEx {
    
    public static void main(String[] args) {
        
        String htmlString = "<html><head><title>My title</title></head>"
                + "<body><center>Body content</center></body></html>";

        boolean valid = Jsoup.isValid(htmlString, Whitelist.basic());
        
        if (valid) {
            
            System.out.println("The document is valid");
        } else {
            
            System.out.println("The document is not valid.");
            System.out.println("Cleaned document");
            
            Document dirtyDoc = Jsoup.parse(htmlString);
            Document cleanDoc = new Cleaner(Whitelist.basic()).clean(dirtyDoc);

            System.out.println(cleanDoc.html());
        }
    }
}
```

In the example, we sanitize and clean HTML data.

```java
String htmlString = "<html><head><title>My title</title></head>"
        + "<body><center>Body content</center></body></html>";
```

The HTML string contains the center element, which is deprecated.  

```java
boolean valid = Jsoup.isValid(htmlString, Whitelist.basic());
```

The `isValid` method determines whether the string is a valid HTML. A white list  
is a list of HTML (elements and attributes) that can pass through the cleaner.  
The Whitelist.basic defines a set of basic clean HTML tags.  

```java
Document dirtyDoc = Jsoup.parse(htmlString);
Document cleanDoc = new Cleaner(Whitelist.basic()).clean(dirtyDoc);
```

With the help of the `Cleaner`, we clean the dirty HTML document.  


## Perform Google search

The following example performs a Google search with Jsoup.

```java
package com.zetcode;

import java.io.IOException;
import java.util.HashSet;
import java.util.Set;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

public class JsoupGoogleSearchEx {

    private static Matcher matcher;
    private static final String DOMAIN_NAME_PATTERN
            = "([a-zA-Z0-9]([a-zA-Z0-9\\-]{0,61}[a-zA-Z0-9])?\\.)+[a-zA-Z]{2,15}";
    private static Pattern patrn = Pattern.compile(DOMAIN_NAME_PATTERN);

    public static String getDomainName(String url) {

        String domainName = "";
        matcher = patrn.matcher(url);
        
        if (matcher.find()) {
            domainName = matcher.group(0).toLowerCase().trim();
        }
        
        return domainName;
    }

    public static void main(String[] args) throws IOException {

        String query = "Milky Way";

        String url = "https://www.google.com/search?q=" + query + "&num=10";

        Document doc = Jsoup
                .connect(url)
                .userAgent("Jsoup client")
                .timeout(5000).get();

        Elements links = doc.select("a[href]");

        Set<String> result = new HashSet<>();

        for (Element link : links) {

            String attr1 = link.attr("href");
            String attr2 = link.attr("class");
            
            if (!attr2.startsWith("_Zkb") && attr1.startsWith("/url?q=")) {
            
                result.add(getDomainName(attr1));
            }
        }

        for (String el : result) {
            System.out.println(el);
        }
    }
}
```

The example creates a search request for the *Milky Way* term. It prints ten  
domain names that match the term.  

```java
private static final String DOMAIN_NAME_PATTERN
        = "([a-zA-Z0-9]([a-zA-Z0-9\\-]{0,61}[a-zA-Z0-9])?\\.)+[a-zA-Z]{2,15}";
private static Pattern patrn = Pattern.compile(DOMAIN_NAME_PATTERN);
```

A Google search returns long links from which we want to get the domain names.  
For this we use a regular expression pattern.  

```java
public static String getDomainName(String url) {

    String domainName = "";
    matcher = patrn.matcher(url);
    
    if (matcher.find()) {
        domainName = matcher.group(0).toLowerCase().trim();
    }
    
    return domainName;
}
```

The `getDomainName` returns a domain name from the search link using the regular  
expression matcher.  

```java
String query = "Milky Way";
```

This is our search term.  

```java
String url = "https://www.google.com/search?q=" + query + "&num=10";
```

This is the URL to perform a Google search.  

```java
Document doc = Jsoup
        .connect(url)
        .userAgent("Jsoup client")
        .timeout(5000).get();
```

We connect to the URL, set a 5 s time out, and send a GET request. A HTML  
document is returned.  

```java
Elements links = doc.select("a[href]");
```

From the document, we select the links.

```java
Set<String> result = new HashSet<>();

for (Element link : links) {

    String attr1 = link.attr("href");
    String attr2 = link.attr("class");
    
    if (!attr2.startsWith("_Zkb") && attr1.startsWith("/url?q=")) {
    
        result.add(getDomainName(attr1));
    }
}
```

We look for links that do not have `class="_Zkb"` attribute and have  
`href="/url?q="`attribute. Note that these are hard-coded values that might  
change in the future.  

```java
for (String el : result) {
    System.out.println(el);
}
```

Finally, we print the domain names to the terminal.
