# 01-introduction-to-java.md

Progress: New
: No
Parent item: Module 0 (not for marks) -- Sept 2-16 -- Java Fundamentals and Version Control (Module%200%20(not%20for%20marks)%20--%20Sept%202-16%20--%20Java%20Fund%2026be7be659d980a1ac65c67180e81c76.md)
Resources: https://github.com/CSC207-UofT/207-course-notes/blob/master/01-introduction-to-java.md

https://docs.oracle.com/javase/tutorial/java/nutsandbolts/index.html
Practice: https://q.utoronto.ca/courses/394773/quizzes/460462
More Resources/Practice: screencapture-q-utoronto-ca-courses-394773-quizzes-460462-history-2025-12-13-16_36_07.pdf

# 1.0 Running a program

Code must be translated into machine code that is eventually executed on the physical hardware.

There are two main ways this translation happens:

- **Interpretation**: The program is read and executed line-by-line by another program called an interpreter. (e.g., Python)
- **Compilation**: The entire program is translated/compiled into machine code ahead of time by a compiler, producing an executable file. (e.g., C)
    - complied directly into machine code corresponding to a particular OS 
    ⇒ not portable : needs to be recompiled for each OS it runs on
- Java (hybrid approach): Java compiler (`javac`) translates source code into **bytecode**, an intermediate form → **Java Virtual Machine (JVM)** then interprets and optimizes this bytecode at runtime.
    - to run a `<file>.java` program (in terminal): compile (`javac <file>.java`) → `<file>.class` contains corresponding bytecode → execute (`java <file>`) runs the program
    - IDEs manage and automate ^ to simplify the development process
    - uses VMs → portability
        
        ⇒ the same `.class` file can run on Windows, macOS, or Linux, as long as a JVM is installed
        

**Virtual Machine (VM):** software application that simulates a computer; consistent environment for programs, regardless of OS

⭐ VM itself is just another application running on an OS, so those OS-specific details still need to be taken care of in the VM code.

```html
Java Applications
---------------
Virtual Machine
---------------
Operating System
---------------
Hardware

------------------------------

Java Applications
---------------
Java Virtual Machine (JVM)
---------------
Operating System
---------------
Hardware
```

# 1.1 First look at Java

When a program is run, actually the class is being run and the `main` method is executed:

```java
class Hello { 
    public static void main(String[] args) { // shortcut: psvm
        // The method body will go here.
    }
}
```

To print into console:

```java
System.out.println(7 + 5);
```

# 1.2 Variables and Types

## Variables

- In Java, every object/value has a type, and so does every variable (unlike in Python)
    - a variable’s type *must* be declared prior to assigning a value; this type can never change → **declaring** a variable: e.g., `int i;`
    - you can assign a value in the same line of code (`int i = 42;`) or assign later so currently, the variable's name is known to Java, space has been reserved to store its value, Java remembers the only type it can refer to, and it is given a default value
        
        Default values:
        
        - int: `0`
        - class types: `null`

Variable Components:

1. The variable's name, which we provide when we declare the variable.
2. The variable's type, which we also provide when we declare the variable.
3. The memory space used to hold the value of the variable.
4. The value of the variable, which can be given using an assignment statement. ← only one that can be changed

Potential variable-related errors:

- not declaring a variable: `i = 42;`
- assigning a value of the wrong type: `int i = 19.6;`
- declaring duplicate variables: `int i = 15; int i = 42;`

# 1.3 Reference Types and Primitive Types

```java
// We've seen an int before.
int age = 21;

// Strings must be double-quoted in Java, unlike Python.
String name = "Jude";

// This type is named boolean in Java, rather than bool (as in Python).
// Its values are true and false in Java (with no capital letter), 
// rather than True and False (as in Python).
boolean graduated = false;

// Type double is like float in Python.
double gpa = 3.82;
```

**reference type** - a Java variable *cannot* hold a value of this type directly within itself and must hold a reference to an object of the type; type begins with an uppercase letter; e.g., `String`

**primitive type** - a Java variable *can* hold a value of this type directly inside itself; type begins with a lowercase letter; e.g., `int`

# 1.4 Strings

- Java `String` literals require double-quotes

```java
String s1 = new String("Hello");
// Creates a nes instance of the String class, regardless whether 
// "Hello" was previously created

String s2 = "bye";
// Java goes in String pool to search for any existing "Hello" object
// If not in String pool, it creates the object and throws into String pool
// If in String pool, Java points s2 to the existing  "Hello" string literal
// => saves memory space

// Thus,
System.out.println(s1 == s2);
// would return false
```

- `String`'s are *immutable*
- `StringBuilder`'s are *mutable*
    - faster to mutate strings than creating new String objects every time a change is needed
- `char` variable types (primitive) are single characters and values must be assigned with single-quotes: `char c = 'x';`

## 1.5 Classes

Instantiating an object:

When Java evaluates the expression `new StringBuilder("Viriyakattiyaporn")`, it:

- allocates memory for the new object,
- evaluates the arguments,
- calls the appropriate constructor, and
- returns a reference to the newly-constructed object.

You can then assign the reference to a variable (`StringBuilder name = new StringBuilder("Viriyakattiyaporn");`), or use it directly (`System.out.println(new StringBuilder("Professor").append(" Horton"));`).

---

### APIs

**Application Programming Interface (API)**: It tells us what methods we can call, what arguments we must send, and what value will be returned. 

- typically does not describe the implementation and focuses more on how client code and use the class

---

Instance methods:

```java
String band = "Arcade Fire";
// Call an instance method via an instance.
int size = band.length(); // "Hey band, you're a String: tell me your length!"
```

Class (`static`) methods:

```java
// Call a class method via the class name.
double x = Math.cos(48); // "Hey Math class, tell me the cosine of 48"
```

# 1.6 Arrays

- Java arrays have a fixed length that is set during construction and can’t be changed afterwards
- Java arrays are reference types → declaring an array variable just creates a variable that can point to an array
- All Java array elements must be of the same type and is declared as such

e.g., `int[] numbers = new int[5];` **constructs** a variable that points to an array of integers of length 5, with default values 0

NOTE: the *type* of the variable is just an integer array, not the length ⇒ any sized integer array can be assigned to the variable throughout the program

Combing array construction and initialization:

`int[] numbers = {1, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024};`

Accessing array elements:

- array indices start at 0
- assigning value to an array position: `numbers[1] = 512;`
- Java arrays don’t support negative indices or splicing

Can store values of different types using `Object` class: 
`Object[] miscellany = new Object[5];`

⇒ can store primitives, created classes, and other array!

Multi-dimensional arrays:

```java
int[][] table;
// We have merely a variable with space for a reference of array of int arrays.
table = new int[50][3];
// Now we have an array of 50 elements, each of which refers to 
// an array of 3 elements, each of which can store an int.

// We have to keep the two different dimensions straight.
// This is legal:
table[49][2] = 123;
// This is not:
table[2][49] = 123;
//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
// Irregularly dimensioned arrays
int[][] irregular;
irregular = new int[3][];
// Now we have an array of 3 elements, each of which can refer to
// an int array, but doesn't yet.
irregular[0] = new int[6];
irregular[1] = new int[99];
irregular[2] = new int[10];
irregular[1][8] = 170;
```

# 1.7 Aliases

**aliases** - variables that reference the same object

- can only be done for reference variable types, NOT for primitives
- side effects (accidentally changing a variable b/c its alias was changed or mutating a parameter passed into a method modifies the original, etc.) may result if the object being referred to by alias(es) are mutable
    
    ^ can be avoided by creating copies of mutable objects when assigning to a new variable
    
    **shallow copy** - creating a copy only of the highest level object (e.g., outer array in a 2-dimensional array)
    
    ```java
    int[][] table = {
        {11, 22},
        {5, 10}
    };
    int[][] copy = new int[2][2];
    for (int i = 0; i < table.length; i++) {
        copy[i] = table[i];
    }
    int[] row = {0, 0};
    copy[0] = row;
    // Changing copy[0] did not change table.  All is right with the world.
    // What happens if we do this?
    copy[1][1] = -99999;
    // changing copy[1][1] does change table: it has -99999 at index [1][1]
    ```
    
    **deep copy** - creating a copy of every level of an object 
    

# 1.8 Control Structures

## if Statements

- Curly braces determine if structure, NOT indentation
- Java doesn't have `and`, `or`, and `not` operators. The equivalent operators in Java are `&&`, `||`, and `!`, respectively.
- The round brackets around the condition are **required** in Java! The body itself is enclosed within curly braces. However, if the body of the if-statement has just a single line, the curly braces are optional. For example:
    
    ```java
    int classSize = 124;
    int sections = 1;
    if (classSize > 500)
        System.out.println("Wow, that's big!"); // curly braces optional here, BUT
        // risk of this:
        sections = 3;               // These lines are OUTSIDE of the if-block!
        classSize = classSize / 3;  // They'll ALWAYS run!
    ```
    

General structure:

```java
int grade = 86;
char letterGrade;
if (grade > 80) {
    letterGrade = 'A';
} else if (grade > 70) {
    letterGrade = 'B';
} else if (grade > 60) {
    letterGrade = 'C';
} else if (grade > 50) {
    letterGrade = 'D';
} else {
    letterGrade = 'F';
}
```

## for Loops

```java
for (initialization; termination; increment) {
    loop body
}
```

- The `*initialization*` is executed once, *before* any iteration begins. It is very often sets a counter to 0, but it can be any statement.
    - common to put the variable declaration in the initialization (e.g., `int i = 1`) because this limits its scope (the part of the code in which we can refer to it) to the loop. The variable disappears from our stack frame as soon as the loop is over, keeping a nice clean namespace
- The `*termination*` is a boolean condition. If it evaluates to true, we execute the loop body and then execute the increment.
- The `*increment*` is usually, as the name suggests, a statement that increments a variable, but it could be any statement.

for Loops for arrays and “collections”:

```java
int[] powers = {1, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024};
for (int p : powers) {
    System.out.println(p);
}
```

Increment shorthands:

```java
x += n;    // Equivalently: x = x + n
y -= n;    // Equivalently: y = y + n
i++;      // Equivalently: i = i + 1
i--;      // Equivalently: i = i - 1
```

NOTE: 

- `++i` is *pre-increment*: the value is increased before it is used.
- `i++` is *post-increment*: the value is increased after it is used.

```java
int i = 5;
int a = ++i; // i becomes 6, then a is assigned 6
System.out.println("i: " + i + ", a: " + a); // Output: i: 6, a: 6

int j = 5;
int b = j++; // b is assigned 5, then j becomes 6
System.out.println("j: " + j + ", b: " + b); // Output: j: 6, b: 5
```

## while Loops

```java
while (condition) {
    ...
}
```

- The condition must be inside round brackets.
- The while-loop's body needs curly braces if it is more than one line long, but it should have curly braces even if it is only one line long.
- NOTE: no semicolon at the end of the block

There is another way for a while-loop to function — with a semicolon, and it involves the increment/decrement operator. Remember that `i++` increments the variable after the condition is checked, while `++i` increments it before it is checked.

```java
int i = 0;
while (i++ < 10);
```

This kind of format of while loop can be used to increment/decrement array indices until the condition is met.

## do-while Loops

The do-while loop checks its condition after the loop runs, ensuring that the loop always runs at least once.

```java
do {
    // your code inside
} while (condition); // Note the semicolon at the end of the block.
```

# 1.9 Parameters

- take notes October 17, 2025