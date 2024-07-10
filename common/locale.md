# Locale 

*Internationalization* is the process of designing an application so that it can  
be adapted to various languages and regions. *Localization* is the process of  
customizing applications for a specific region or language.  

Locale represents a specific geographical, political, or cultural region.  

Locale-sensitive data include:

- messages
- dates and times
- numbers
- currencies
- measurements
- phone numbers
- names
- postal addresses

# Default locale

The default locale is determined with `Locale.getDefault`.

```java
import java.util.Locale;

void main() {

    var defLoc = Locale.getDefault();
    System.out.println(defLoc.getDisplayCountry());
    System.out.println(defLoc.getDisplayLanguage());
    System.out.println(defLoc.getDisplayName());
    System.out.println(defLoc.getISO3Country());
    System.out.println(defLoc.getISO3Language());
    System.out.println(defLoc.getLanguage());
    System.out.println(defLoc.getCountry());

    System.out.println("------------------------");

    var skLoc = new Locale("SK", "sk");
    System.out.println(skLoc.getDisplayCountry());
    System.out.println(skLoc.getDisplayLanguage());
    System.out.println(skLoc.getDisplayName());
    System.out.println(skLoc.getISO3Country());
    System.out.println(skLoc.getISO3Language());
    System.out.println(skLoc.getLanguage());
    System.out.println(skLoc.getCountry());
}
```

The program prints the attributes of a default locale and a Slovak locale.

```java
var defLoc = Locale.getDefault();
System.out.println(defLoc.getDisplayCountry());
System.out.println(defLoc.getDisplayLanguage());
System.out.println(defLoc.getDisplayName());
```

We get the default locale and print the display country name, language, and  
name.


## Locale constants

There are a few built-in locale constants such as `Locale.US`.

```java
import java.text.NumberFormat;
import java.util.Locale;

void main() {

    double n = 1240.35;

    NumberFormat nf = NumberFormat.getInstance(Locale.US);
    System.out.println(nf.format(n));

    NumberFormat nf2 = NumberFormat.getInstance(Locale.FRANCE);
    System.out.println(nf2.format(n));

    NumberFormat nf3 = NumberFormat.getInstance(Locale.GERMAN);
    System.out.println(nf3.format(n));
}
```

The program prints a number in `Locale.US`, `Locale.FRANCE`, and `Locale.GERMAN`  
locales.  

```java
NumberFormat nf = NumberFormat.getInstance(Locale.US);
```

The `NumberFormat.getInstance` returns a general-purpose number format for the  
specified locale.  

```java
System.out.println(nf.format(n));
```

We pass the value to the `NumberFormat's` format method.  

## Locale.Builder

Locales can be created with `Locale.Builder`.

```java
import java.text.NumberFormat;
import java.util.Locale;

public class LocaleEx {

    public static void main() {

        double n = 1240.35;

        var loc = new Locale.Builder()
                .setLanguage("sk")
                .setRegion("SK")
                .build();

        NumberFormat nf = NumberFormat.getInstance(loc);
        System.out.println(nf.format(n));

        var loc2 = new Locale.Builder()
                .setLanguage("ja")
                .setRegion("JP")
                .build();

        NumberFormat nf2 = NumberFormat.getInstance(loc2);
        System.out.println(nf2.format(n));
    }
}
```

The program localizes a value for Slovak and Japanese languages. The locales are  
created with a builder.  

```java
var loc = new Locale.Builder()
    .setLanguage("sk")
    .setRegion("SK")
    .build();
```

A locale is built with the builder. We set the language with setLanguage and the  
region with `setRegion`.  


## Locale constructor

There are three constructors for creating a `Locale` object.

```java
Locale(String language)
Locale(String language, String country)
Locale(String language, String country, String variant)
```

We can specify language, country, and variants as parameters.

```java
import java.math.BigDecimal;
import java.text.NumberFormat;
import java.util.Locale;

void main() {

    var val = new BigDecimal("2530.45");

    var skLoc = new Locale("sk", "SK");
    var huLoc = new Locale("hu", "HU");
    var ruLoc = new Locale("ru", "RU");

    NumberFormat cf1 = NumberFormat.getCurrencyInstance(skLoc);
    System.out.println(cf1.format(val));

    NumberFormat cf2 = NumberFormat.getCurrencyInstance(huLoc);
    System.out.println(cf2.format(val));

    NumberFormat cf3 = NumberFormat.getCurrencyInstance(ruLoc);
    System.out.println(cf3.format(val));
}
```

In the example, we print a currency value in Slovak, Hungarian, and Russian  
locales.  

```java
var val = new BigDecimal("2530.45");
```

For currency values, we should use `BigDecimal`.

```java
NumberFormat cf1 = NumberFormat.getCurrencyInstance(skLoc);
```

To format a currency value, we use the `NumberFormat.getCurrencyInstance` to  
which we pass the locale.  


## Locale format datetime

With Locale and `DateTimeFormatter`, we can format datetime values.

```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.time.format.FormatStyle;
import java.util.Locale;

void main() {

    var now = LocalDateTime.now();
    var dtf1 = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.MEDIUM)
            .withLocale(Locale.FRANCE);
    System.out.println(now.format(dtf1));

    var dtf2 = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.MEDIUM)
            .withLocale(Locale.US);
    System.out.println(now.format(dtf2));

    var dtf3 = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.MEDIUM)
            .withLocale(Locale.TRADITIONAL_CHINESE);
    System.out.println(now.format(dtf3));
}
```

In the program, we format the current datetime in French, US, and Chinese  
locales.  

```java
var dtf1 = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.MEDIUM)
    .withLocale(Locale.FRANCE);
```

We choose a datetime format style with `ofLocalizedDateTime` and set the locale  
with `withLocale`.  


## Locale ResourceBundle

A resource bundle is a Java properties file that contains locale-specific data.  
We localize messages with resource bundles. The files are located in the 
`src/main/resources` directory.  

```
w1=Earth
w2=ocean
```

This is the default properties file; it is typically in English language. We  
have two words inside the file.  

```
w1=Erde
w2=ozean
```

The `words_de.properties` file contains words in German language.

```
resources/words_ru.properties
w1=Земля
w2=океан
```

The `words_ru.properties` file contains words in Russian language.

When using IntelliJ IDEA, we need to change the encoding of the properties file  
to utf-8; the default is ISO-8859-1  

```java
import java.nio.charset.Charset;
import java.util.Locale;
import java.util.ResourceBundle;

void main() {

    Locale[] locales = {
            Locale.GERMAN,
            Locale.of("ru", "RU"),
            Locale.ENGLISH
    };

    System.out.println("w1:");

    for (Locale locale : locales) {

        getWord(locale, "w1");
    }

    System.out.println("w2:");

    for (Locale locale : locales) {

        getWord(locale, "w2");
    }

    System.out.println(Charset.defaultCharset());
}

void getWord(Locale curLoc, String key) {

    ResourceBundle words = ResourceBundle.getBundle("main/resources/words", curLoc);
    String value = words.getString(key);

    System.out.printf("Locale: %s, Value: %s %n", curLoc, value);
}
```

In the code example, we print all the words used in three resource bundles.

```java
ResourceBundle words = ResourceBundle.getBundle("main/resources/words", curLoc);
```

With the `ResourceBundle.getBundle` method, we get the bundle for the currently  
used locale.  

```java
String value = words.getString(key);
```

From the bundle, we retrieve values with `getString`.

```
w1:
Locale: de, Value: Erde 
Locale: ru_RU, Value: Земля 
Locale: en, Value: Earth 
w2:
Locale: de, Value: ozean 
Locale: ru_RU, Value: океан 
Locale: en, Value: ocean 
```
