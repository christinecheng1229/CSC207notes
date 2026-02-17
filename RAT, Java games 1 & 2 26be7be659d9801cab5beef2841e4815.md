# RAT, Java games 1 & 2

Progress: New
: No
Parent item: Module 0 (not for marks) -- Sept 2-16 -- Java Fundamentals and Version Control (Module%200%20(not%20for%20marks)%20--%20Sept%202-16%20--%20Java%20Fund%2026be7be659d980a1ac65c67180e81c76.md)
Practice: https://q.utoronto.ca/courses/394773/quizzes/473946 | https://q.utoronto.ca/courses/394773/pages/m0-java-games-part-1-2 | https://q.utoronto.ca/courses/394773/pages/m0-java-games-part-2-2
More Resources/Practice: iRAT%201.pdf

# RAT

([https://q.utoronto.ca/courses/394773/quizzes/473946/history?version=1](https://q.utoronto.ca/courses/394773/quizzes/473946/history?version=1))

- Q1) What does `public static void main(String[] args)`(PSVM) represent?
    
    starting point of the program
    
- Q2) What is the output of 
`int x = 10;` 
`System.out.prinln(x/3);`?
    
    3
    
    - `int`<-  Java types remain unchanged

```java
public class Car {
	String model;
	public Car(String m) {
		model = m;
	}
	
	public static void main(String[] args) {
		Car c = new Car("Toyota");
		System.out.println(c.model);
	}
}
```

- Q3) What is the result of this (^) code?
    
    Toyota
    
    - `this.model` is not necessary, but can be helpful to explicitly specify model refers to the (instance attribute) String model (in case another object is also named model)
    - all constructors calls the one class above (`super();`)
    - java creates a empty constructor (`public Person() {super();}`) in the absence of ANY constructors

# Java Games 1

([https://q.utoronto.ca/courses/394773/pages/m0-java-games-part-1-2](https://q.utoronto.ca/courses/394773/pages/m0-java-games-part-1-2))

```java
public class IfTest {
     public static void main(String[] args) {
          int x = 10;
          if (x < 5)
               System.out.println("Low");
          else if (x < 15)
               System.out.println("Medium");
          else
               System.out.println("High");
     }
}
```

- Activity 1: What is the output of (^)?
    
    Medium
    
    - without curly braces it assumes the next line (until semicolon) is the rest of the if block and functions as normal if, else if, else structure

```java
public class SwitchTest {
     public static void main(String[] args) {
          int val = 2;
          switch (val) {
               case 1:
                    System.out.print("One ");
               case 2:
                    System.out.print("Two ");
               case 3:
                    System.out.print("Three ");
                    break;
               default:
                    System.out.print("Default");
          }
     }
}
```

- Activity 2: What is the output of (^)?
    
    Two Three
    
    - executes of all blocks of code after `case 2` match until the `break`

```java
public class LoopScope {
     public static void main(String[] args) {
          for (int i = 0; i < 3; i++) {
               int x = 10;
               System.out.print(x + " ");
          }
          // System.out.println(x);
     }
}
```

- Activity 3: What is the output of (^) when uncommented?
    
    compile error
    
    - `x` is local to the for loop → java has no clue what it is → compile error (without running the program/assigning values, Java knows x doesn’t exist outside of loop)
    - **compile error** is more so a “spell-check” that doesn’t assign vales and checks mostly syntax
    - **runtime error** is about logic (e.g., dividing by 0) that occurs after (e.g., when values have been assigned)

```java
public class WhileTest {
     public static void main(String[] args) {
          int i = 5;
          while (i > 0) {
               System.out.print(i + " ");
               i--;
          }
     }
}
```

- Activity 4: What is the output of (^)?
    
    5 4 3 2 1
    

```java
public class DoWhileTest {
     public static void main(String[] args) {
          int i = 0;
          do {
               System.out.println("Hello");
          } while (i > 0);
     }
}
```

- Activity 5: (^) How many times does “Hello” print?
    
    1
    
    - `do` executes once by default before checking condition

```java
public class BreakTest {
     public static void main(String[] args) {
          for (int i = 0; i < 5; i++) {
               if (i == 3) break;
               System.out.print(i + " ");
          }
     }

}
```

- Activity 6: What is the output of (^)?
    
    0 1 2
    
    - `break` ends the for loop → ends the program

```java
public class ContinueTest {
     public static void main(String[] args) {
          for (int i = 0; i < 5; i++) {
               if (i == 2) continue;
               System.out.print(i + " ");
          }
     }
}
```

- Activity 7: What is the output of (^)?
    
    0 1 3 4
    
    - `continue` skips rest of for loop and continues to the following iterations normally

```java
public class NestedIf {
     public static void main(String[] args) {
          int score = 75;
          if (score >= 50)
               if (score >= 80)
                    System.out.println("Distinction");
               else
                    System.out.println("Pass");
          else
               System.out.println("Fail");
     }
}
```

- Activity 8: What is the output of (^)?
    
    Pass
    
    - functions as normal nested if else structures even w/o curly brackets

```java
public class LoopNoBody {
     public static void main(String[] args) {
          int i = 0;
          while (++i < 3);
          System.out.println(i);
     }
}
```

- Activity 9: What is the output (^)?
    
    3
    
    ```java
    i = 3;
    System.out.println(i++);
    // prints 3, value of i afterwards is 4
    ////////////////////
    ++i
    // adds to i and assigns that value to object i
    
    ```
    

```java
public class SwitchDefaultFirst {
     public static void main(String[] args) {
          int x = 1;
          switch (x) {
               default:
                    System.out.println("Default");
                    break;
               case 1:
                    System.out.println("One");
          }
     }
}
```

- Activity 10: What is the output of (^)?
    
    One
    

# Java Games 2

```java
public class Counter {
      private static int count = 0;
    
      public void increment() {
          count++;
	    }
    
      public int getCount() {
          return count;
      }
    
      public static void main(String[] args) {
          Counter a = new Counter();
          Counter b = new Counter();
          a.increment();
          b.increment();
          System.out.println(a.getCount());
      }
}
```

- Activity 1: What is the output of (^)?
    
    2
    
    - `static` variables are created before program even runs
    - object `a` and `b` shares the count variable across class `Counter`
    - any instance of `getCount()` gives global value of count

```java
public class Demo {

     int x = 5;

     public Demo() {
          System.out.println(x);
          x = 10;
     }

     public static void main(String[] args) {
          new Demo();
     }
}
```

- Activity 2: What is the output of (^)?
    
    5
    
    - first line of `Demo()` is `sout()` and `x` only has a value of 5

```java
class A {
     void greet() {
          System.out.println("Hello from A");
     }
}

class B extends A {
     void greet() {
          System.out.println("Hello from B");
     }
}

public class TestOverride {
     public static void main(String[] args) {
          A obj = new B();
          obj.greet();
     }
}
```

- Activity 3: What is the output of (^)?
    
    Hello from B
    
    - `obj` is an instance of 3 classes: `Object`, `A`, `B`
    - Java assumes the lowest (descendant/child) class is the “updated version” or **overridden** version → uses `B.greet()`
    - NOTE: if class `A` didn’t have a `greet()` method, Java assumes it was inherited from the superclass (`Object` in this case) ← Java lookup rules
        - lookup rules only apply to instance methods, NOT static methods and variables

```java
class Parent {

     static void sayHi() {

          System.out.println("Hi from Parent");

     }

}

class Child extends Parent {

     static void sayHi() {

          System.out.println("Hi from Child");

     }

}

public class TestStatic {

     public static void main(String[] args) {

          Parent p = new Child();

          p.sayHi();

     }

}
```

- Activity 4: What is the output of (^)?
    
    (B) Hi from Parent
    

```java
class Parent {
     Parent() {
          System.out.println("Parent constructor");
     }
}

class Child extends Parent {
     int y = printY();

     Child() {
          System.out.println("Child constructor");
     }

     int printY() {
          System.out.println("Initializing y");
          return 42;
     }
}

public class TestInit {
     public static void main(String[] args) {
          new Child();
     }
}
```

- Activity 5: What is the output of (^)?
    
    A) Parent → Initializing y → Child