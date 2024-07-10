# Java datetime

The original Java datetime API was poor. In Java 8, it was replaced with modern  
API.

The following classes are deprecated:  

- java.util.Date
- java.util.Calendar
- java.util.GregorianCalendar

The modern Java datetime API is located in the `java.time` package.  

## Modern API

Key features:

* *Clear and Specific Classes:* Instead of a single class like `Date`, the API  
  provides dedicated classes for different aspects of date and time:  
    * `LocalDate`: Represents a date (year, month, day) without time zone or  
      time information. (e.g., 2024-07-10)  
    * `LocalTime`: Represents a time (hour, minute, second, nanosecond) without  
      date information. (e.g., 14:57)  
    * `LocalDateTime`: Combines date and time without time zone information.  
      (e.g., 2024-07-10T14:57)  
* *Time Zones:* For time zone awareness, the API provides classes like:  
    * `ZonedDateTime`: Represents date and time with a specific time zone.  
      (e.g., 2024-07-10T14:57:23+02:00[CEST])  
    * `OffsetDateTime`: Represents date and time with an offset from UTC  
      (Coordinated Universal Time). (e.g., 2024-07-10T14:57:23+02:00)  
* *Immutability:* Most classes in the API are immutable, meaning their values  
  cannot be changed after creation. This ensures thread safety and simplifies  
  code reasoning.  
* *Formatting and Parsing:* Dedicated classes like `DateTimeFormatter` allow  
  for easy formatting of date and time objects into various string  
  representations and vice versa. (e.g., formatting a `LocalDateTime` to  
  "YYYY-MM-DD HH:mm")  
* *Temporal API:*  Provides a more advanced layer for framework developers,  
  enabling operations like querying, adjusting, and interoperating between  
  different date and time classes.  
  
Overall, the modern Java datetime API offers a powerful and intuitive way to  
handle dates and times in your Java applications, promoting clarity, thread  
safety, and easier manipulation of date and time data.  



## Current datetime 

```java
import java.time.LocalDateTime;
import java.time.ZoneId;
import java.time.ZonedDateTime;
import java.util.Date;

void main() {

    Date dt = new Date();
    System.out.println(dt);

    // Java 8
    LocalDateTime ldt = LocalDateTime.now();
    System.out.println(ldt);

    ZonedDateTime zdt = ZonedDateTime.now(ZoneId.of("Europe/Bratislava"));
    System.out.println(zdt);
}
```

## Instant

`Instant` represents a specific moment in time on the timeline. It's akin to a  
single point on a never-ending line. Unlike other date and time classes,  
`Instant` doesn't inherently include time zone information. Instead, it measures  
time as the number of seconds and nanoseconds elapsed since a specific point in  
time, known as the epoch.  

The epoch is January 1st, 1970, at 00:00:00 Coordinated Universal Time (UTC).  
Positive Instant values represent times after the epoch, while negative values  
indicate times before.  

Common use cases for `Instant` include:

- Recording timestamps for events within an application.  
- Storing timestamps in databases where UTC is the preferred time format.  
- Performing calculations based on the number of seconds or nanoseconds elapsed  
  since a specific point in time.  


```java
import java.time.Instant;
import java.time.ZoneId;
import java.time.temporal.ChronoUnit;

void main() {

    var timestamp = Instant.now();
    System.out.println("The current timestamp: " + timestamp);

    System.out.printf("Unix time: %d%n", timestamp.toEpochMilli());

    //Now minus five days
    var minusFive = timestamp.minus(5, ChronoUnit.DAYS);
    System.out.println("Now minus five days:" + minusFive);

    var atZone = timestamp.atZone(ZoneId.of("GMT"));
    System.out.printf("GMT: %s%n", atZone);

    var yesterday = Instant.now().minus(24, ChronoUnit.HOURS);
    System.out.println("Yesterday: " + yesterday);
}
```

## Unix time 

Unix time (also known as POSIX time or epoch time) is a system for describing a  
point in time, defined as the number of seconds that have elapsed since 00:00:00  
Coordinated Universal Time (UTC), Thursday, 1 January 1970, minus the number of  
leap seconds that have taken place since then  


```java
import java.time.Instant;

void main() {

    long unixTime = System.currentTimeMillis() / 1000L;
    System.out.println(unixTime);

    // Since Java 8

    long unixTime2 = Instant.now().getEpochSecond();
    System.out.println(unixTime2);
}
```

## ZonedDateTime 

The `ZonedDateTime` class represents a specific date and time along with its  
corresponding time zone. It essentially combines the functionalities of  
`LocalDateTime` (date and time without time zone) and `ZoneId` (time zone identifier).  

```java
import java.time.ZoneId;
import java.time.ZoneOffset;
import java.time.ZonedDateTime;

void main() {

    var zbrat = ZonedDateTime.now(ZoneId.of("Europe/Bratislava"));
    var zmosc = ZonedDateTime.now(ZoneId.of("Europe/Moscow"));

    System.out.println(zbrat);
    System.out.println(zmosc);

    var utc = ZonedDateTime.now(ZoneOffset.UTC);
    System.out.println(utc);
}
```

## DateTimeFormatter 

We can format `LocalDate` values with `FormatStyle.SHORT`, `FormatStyle.MEDIUM`,  
`FormatStyle.LONG`, `FormatStyle.FULL` format styles.  

```java
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.time.format.FormatStyle;
import java.util.Locale;

void main() {

    Locale.setDefault(Locale.ENGLISH);

    var now = LocalDate.now();

    var dtf1 = DateTimeFormatter.ofLocalizedDate(FormatStyle.SHORT);
    var dtf2 = DateTimeFormatter.ofLocalizedDate(FormatStyle.MEDIUM);
    var dtf3 = DateTimeFormatter.ofLocalizedDate(FormatStyle.LONG);
    var dtf4 = DateTimeFormatter.ofLocalizedDate(FormatStyle.FULL);

    System.out.println(dtf1.format(now));
    System.out.println(dtf2.format(now));
    System.out.println(dtf3.format(now));
    System.out.println(dtf4.format(now));
}
```

Custom formats can be defined with `DateTimeFormatter.ofPattern`.

```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

void main() {

    Locale.setDefault(Locale.ENGLISH);

    var now = LocalDateTime.now();

    var dtf1 = DateTimeFormatter.ofPattern("yyyy-MM-dd");
    var dtf2 = DateTimeFormatter.ofPattern("E, MMM dd yyyy");
    var dtf3 = DateTimeFormatter.ofPattern("EEEE, MMM dd, yyyy HH:mm:ss a");

    System.out.println(dtf1.format(now));
    System.out.println(dtf2.format(now));
    System.out.println(dtf3.format(now));
}
```

Localized datetime formats are created with `ofPattern` and `Locale`.

```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.Locale;

void main() {

    var now = LocalDateTime.now();

    String pattern = "EEEE, MMM dd, yyyy HH:mm:ss a";
    var dtf1 = DateTimeFormatter.ofPattern(pattern, Locale.CHINA);
    var dtf2 = DateTimeFormatter.ofPattern(pattern, Locale.of("RU", "ru"));
    var dtf3 = DateTimeFormatter.ofPattern(pattern, Locale.of("SK", "sk"));

    System.out.println(dtf1.format(now));
    System.out.println(dtf2.format(now));
    System.out.println(dtf3.format(now));
}
```

Parsing datetime objects from strings with `parse`.  

```java
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.time.temporal.TemporalAccessor;
import java.util.Locale;

void main() {

    Locale.setDefault(Locale.ENGLISH);

    String d = "2023-10-26";

    DateTimeFormatter dtf = DateTimeFormatter.ISO_DATE;
    TemporalAccessor ta = dtf.parse(d);
    LocalDate ld = LocalDate.from(ta);
    System.out.println(ld);

    String sd1 = "2018-01-04";
    LocalDate ld1 = LocalDate.parse(sd1);
    System.out.println("Date: " + ld1);

    String sdatetime = "2017-08-16T16:34:10";
    LocalDateTime ldt = LocalDateTime.parse(sdatetime);
    System.out.println("Datetime: " + ldt);

    DateTimeFormatter dtfmt = DateTimeFormatter.ofPattern("dd MMM yyyy");
    String anotherDate = "14 Aug 2017";
    LocalDate lds = LocalDate.parse(anotherDate, dtfmt);
    System.out.println(anotherDate + " parses to " + lds);
}
```

## DateTime arithmetic 


```java
import java.time.LocalDateTime;

void main() {

    LocalDateTime now = LocalDateTime.now();
    System.out.println(now);

    // LocalDateTime addition
    System.out.println("Adding 4 years: " + now.plusYears(4));
    System.out.println("Adding 11 months: " + now.plusMonths(11));
    System.out.println("Adding 54 days: " + now.plusDays(54));
    System.out.println("Adding 3 hours: " + now.plusHours(3));
    System.out.println("Adding 30 minutes: " + now.plusMinutes(30));
    System.out.println("Adding 45 seconds: " + now.plusSeconds(45));
    System.out.println("Adding 40000 nanoseconds: " + now.plusNanos(40000));

    System.out.println("-------------------------------------");

    // LocalDateTime subtraction
    System.out.println("Subtracting 4 years: " + now.minusYears(4));
    System.out.println("Subtracting 11 months: " + now.minusMonths(11));
    System.out.println("Subtracting 54 days: " + now.minusDays(54));
    System.out.println("Subtracting 3 hours: " + now.minusHours(3));
    System.out.println("Subtracting 30 minutes: " + now.minusMinutes(30));
    System.out.println("Subtracting 45 seconds: " + now.minusSeconds(45));
    System.out.println("Subtracting 40000 nanoseconds: " + now.minusNanos(40000));
}
```

Borodino battle:  

```java
import java.time.LocalDate;

import static java.time.temporal.ChronoUnit.DAYS;

void main() {

    LocalDate now = LocalDate.now();
    LocalDate borodinoBattle = LocalDate.of(1812, 9, 7);

    long passed_days = DAYS.between(borodinoBattle, now);
    System.out.println(passed_days);
}
```

## The until method 

With the `until` method, we can compute the time until another time in terms of  
the specified unit.  

```java
import java.time.LocalDateTime;
import java.time.temporal.ChronoUnit;

void main() {

    LocalDateTime now = LocalDateTime.now();
    LocalDateTime xmas = LocalDateTime.of(now.getYear(), 12, 24, 0, 0 ,0);

    System.out.println(now);
    System.out.println(xmas);

    System.out.printf("%s hours%n", now.until(xmas, ChronoUnit.HOURS));
    System.out.printf("%s minutes%n", now.until(xmas, ChronoUnit.MINUTES));
    System.out.printf("%s seconds%n", now.until(xmas, ChronoUnit.SECONDS));
}
```

## TemporalAdjusters 

TemporalAdjusters are used for modifying temporal objects. They allow to find  
the first or last day of the week, month, or year; the next or previous day of  
week and so on.  

```java
import java.time.DayOfWeek;
import java.time.LocalDate;
import java.time.temporal.TemporalAdjusters;

void main() {

    var localDate = LocalDate.now();
    System.out.printf("today: %s%n", localDate);

    var date1 = localDate.with(TemporalAdjusters.firstDayOfMonth());
    System.out.printf("first day of month: %s%n", date1);

    var date2 = localDate.with(TemporalAdjusters.lastDayOfMonth());
    System.out.printf("last day of month: %s%n", date2);

    var date3 = localDate.with(TemporalAdjusters.next(DayOfWeek.MONDAY));
    System.out.printf("next Monday: %s%n", date3);

    var date4 = localDate.with(TemporalAdjusters.firstDayOfNextMonth());
    System.out.printf("first day of next month: %s%n", date4);

    var date5 = localDate.with(TemporalAdjusters.lastDayOfYear());
    System.out.printf("last day of year: %s%n", date5);

    var date6 = localDate.with(TemporalAdjusters.firstDayOfYear());
    System.out.printf("first day of year: %s%n", date6);

    var date7 = localDate.with(TemporalAdjusters.lastInMonth(DayOfWeek.SUNDAY));
    System.out.printf("last Sunday of month: %s%n", date7);
}
```

## Islamic date

```java
import java.time.LocalDate;
import java.time.chrono.HijrahDate;

void main() {

    var nowIslamic = HijrahDate.now();
    System.out.println("Islamic date: " + nowIslamic);

    var nowGregorian = LocalDate.now();
    System.out.println("Gregorian date: " + nowGregorian);
}
```
