# Scope

*Scope* in Java refers to the region of a program where a variable or other identifier   
is visible and can be used. It determines the accessibility and lifetime of a variable.  


The following constructs have their own scope:  

1. **Code Blocks:**
   - Any code enclosed within curly braces `{}` has its own scope.
   - Variables declared within a code block are only accessible within that block.
   - Examples:
     - `if` statements
     - `for` loops
     - `while` loops
     - `try-catch` blocks
     - Methods

2. **Methods:**
   - Variables declared within a method are only accessible within that method.
   - Parameters passed to a method also have their own scope within the method.

3. **Classes:**
   - Variables declared within a class are accessible throughout the class, including
     within methods and constructors.
   - However, if a variable is declared as `private`, it can only be accessed within
     the class itself.

4. **Interfaces:**
   - Variables declared within an interface are implicitly `public`, `static`, and `final`.
   - They can be accessed from anywhere within the class that implements the interface.


