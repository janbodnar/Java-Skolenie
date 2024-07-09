# Lambdas 

A *lambda expression* is a short block of code which takes in parameters and  
returns a value. Lambda expressions are similar to methods, but they do not need  
a name and can be implemented right in the body of a method.  

The following is the basic syntax for a lambda expression in Java:  

```java
(parameters) -> expression
(parameters) -> { statements; }
```

Lambda expression allow to create more concise code in Java.  

The declaration of the type of the parameter is optional; the compiler can infer  
the type from the value of the parameter. For a single parameter the parentheses  
are optional; for multiple parameters, they are required.  

The curly braces are optional if there is only one statement in an expression  
body. Finally, the return keyword is optional if the body has a single  
expression to return a value; curly braces are required to indicate that the  
expression returns a value.

## Arrays.sort method

```java
import java.util.Arrays;

void main() {

    String[] words = { "kind", "massive", "atom", "car", "blue" };
    Arrays.sort(words, (String s1, String s2) -> (s1.compareTo(s2)));
    System.out.println(Arrays.toString(words));
}
```

In the example, we define an array of strings. The array is sorted using the  
Arrays.sort method and a lambda expression.  


## Swing ActionListener

Rather than creating an anonymous class for an event handler, we can use a  
shorter syntax with lambda expression.  

```java
package com.zetcode;

import javax.swing.GroupLayout;
import javax.swing.JButton;
import javax.swing.JComponent;
import javax.swing.JFrame;
import java.awt.EventQueue;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class QuitButtonEx extends JFrame {

    public QuitButtonEx() {

        initUI();
    }

    private void initUI() {

        var quitButton = new JButton("Quit");

//        quitButton.addActionListener(new ActionListener() {
//            @Override
//            public void actionPerformed(ActionEvent e) {
//                System.exit(0);
//            }
//        });

        quitButton.addActionListener(_ -> System.exit(0));

        createLayout(quitButton);

        setTitle("Quit button");
        setSize(300, 200);
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


## Interfaces

Lambda expressions are used primarily to define an inline implementation of a  
functional interface, i.e., an interface with a single method only. Interfaces  
are abstract types that are used to enforce a contract.  

```java
interface GreetingService {

    void greet(String message);
}

void main() {

    GreetingService gs = (String msg) -> {
        System.out.println(msg);
    };

    gs.greet("Good night");
    gs.greet("Hello there");
}
```
In the example, we create a greeting service with the help of a lambda  
expression.  

```java
interface GreetingService {

    void greet(String message);
}
```

Interface `GreetingService` is created. All objects implementing this interface  
must implement the greet method.  

```java
GreetingService gs = (String msg) -> {
    System.out.println(msg);
};
```

We create an object that implements `GreetingService` with a lambda expression.  
The object has a method that prints a message to the console.  

```java
gs.greet("Good night");
```

We call the object's greet method, which prints a give message to the console.  

## Common functional interfaces

There are some common functional interfaces, such as `Function`, `Consumer`,  
or `Supplier`.

```java
import java.util.function.Function;

    void main() {

        Function<Integer, Integer> square = (Integer x) -> x * x;
        System.out.println(square.apply(5));
    }
```

The example uses a lambda expression to compute squares of integers.

```java
Function<Integer, Integer> square = (Integer x) -> x * x;
System.out.println(square.apply(5));
```

`Function` is a function that accepts one argument and produces a result. The  
operation of the lamda expression produces a square of the given integer.  

```java
import java.util.ArrayList;
import java.util.function.Function;

void main() {

    var words = new ArrayList<String>();
    words.add("sky");
    words.add("warm");
    words.add("winter");
    words.add("cloud");
    words.add("pen");
    words.add("den");
    words.add("tree");
    words.add("sun");
    words.add("silk");

    Function<String, Integer> words2len = word -> word.length();

    var res = words.stream().map(words2len).toList();
//    var res = words.stream().map(word -> word.length()).toList();
    System.out.println(res);
}
```


## Predicate 

Represents a predicate (boolean-valued function) of one argument.  

```java
import java.util.ArrayList;
import java.util.function.Predicate;

void main() {

    var words = new ArrayList<String>();
    words.add("sky");
    words.add("warm");
    words.add("winter");
    words.add("cloud");
    words.add("pen");
    words.add("den");
    words.add("tree");
    words.add("sun");
    words.add("silk");

    Predicate<String> hasThreeChars = word -> word.length() == 3;
    words.removeIf(hasThreeChars);
//    words.removeIf(word -> word.length() == 3);

    System.out.println(words);
}
```


## Filtering data

Lambda expression are often used in methods, which expects methods as parameters.  

```java
import java.util.List;
import java.util.stream.Collectors;
import java.util.function.Predicate;
import java.util.regex.Pattern;

// class Helpers {

//     public boolean emailIsPost(User u) {

//         if (u.email().matches(".*post\\.com")) {
//             return true;
//         } else {
//             return false;
//         }
//     }
// }

// Predicate<User> emailIsPost = (User u) -> u.email().matches(".*post.com");
// Predicate<User> emailIsPost = (User u) -> u.email().matches(Pattern.quote(".*post.com"));

void main() {

    List<User> users = List.of(
            new User("Jack", "jack234@gmail.com"),
            new User("Peter", "pete2@post.com"),
            new User("Lucy", "lucy17@gmail.com"),
            new User("Robert", "bob56@post.com"),
            new User("Martin", "mato4@imail.com"));

    List<User> res = users.stream()
            .filter(user -> user.email().matches(".*post.com"))
            .collect(Collectors.toList());

    // Helpers hlps = new Helpers();

    // List<User> res = users.stream()
    // .filter(emailIsPost)
    // .collect(Collectors.toList());

    res.forEach(u -> System.out.println(u.name()));
}

record User(String name, String email) {
}
```

The example creates a stream of `User` objects. It filters those which match a
specific regular expression.  

```java
List<User> res = users.stream()
        .filter(user -> user.email().matches(".*post.com"))
        .collect(Collectors.toList());
```

In the filter predicate, we choose emails that match the `.*post.com` pattern.   
The predicate is a lambda expression.  

```java
result.forEach(u -> System.out.println(u.name()));
```

Also, the method passed to the `ForEach` is a lambda expression.  


Alternative in Python:  

```python
from collections import namedtuple
import re

User = namedtuple('User', 'name email')


# def emailIsPost(user: User):

#     pattern = re.compile(r'.*post.com')
#     if re.fullmatch(pattern, user.email):
#         return True
#     else:
#         return False

users = [
    User("Jack", "jack234@gmail.com"),
    User("Peter", "pete2@post.com"),
    User("Lucy", "lucy17@gmail.com"),
    User("Robert", "bob56@post.com"),
    User("Martin", "mato4@imail.com")
]


pattern = re.compile(r'.*post.com')
res = list(filter(lambda u: re.fullmatch(pattern, u.email), users))
print(res)
```
