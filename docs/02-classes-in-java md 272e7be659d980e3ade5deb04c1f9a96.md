# 02-classes-in-java.md

Progress: New
: No
Parent item: Module 1 -- Sept 17-30 -- Java OOP (Module%201%20--%20Sept%2017-30%20--%20Java%20OOP%2026be7be659d980358a36cfb6580c99bc.md)
Resources: https://github.com/CSC207-UofT/207-course-notes/blob/master/02-classes-in-java.md

https://github.com/CSC207-UofT/207-course-notes/blob/master/code/Monster.java

https://docs.oracle.com/javase/tutorial/java/javaOO/
More Resources/Practice: screencapture-q-utoronto-ca-courses-394773-quizzes-460464-history-2025-12-13-17_22_13.pdf

# 2.2 Variables

- **Instance variables**: variables belong to each *instance* of a class; exists when an instance is contructed (using `new`)
- **Class variables (`static` variables)**: variables shared by *all instances* of a class

# 2.3 Access Modifiers

[https://docs.oracle.com/javase/tutorial/java/javaOO/accesscontrol.html](https://docs.oracle.com/javase/tutorial/java/javaOO/accesscontrol.html)

- for attributes and/or methods of a class
- `public`: can be accessed from outside a class
- `private`: cannot be accessed from outside a class
- `protected`: accessible to the entire package and any subclasses of a class, but not to anything else
- `package-protected`: default access modifier (in the absence of); `protected` access but excludes subclass access from outside package

# 2.4 Constructors

- methods with no return type (not even `void`), called whenever a new instance of a class is created
- `this`: refers to object whose method is being executed (ie., object we are creating an instance of)
- can be [overloaded](02-classes-in-java%20md%20272e7be659d980e3ade5deb04c1f9a96.md) (create as many you wish within a class) as long as there are different method signatures (# of arguments, argument types, etc.)
    
    ```java
    public int my_method(int something, int something_else){
        return something + something_else;
    }
    
    public int my_method(int something){
        return my_method(something, 1);
    }
    ```
    

## Object Creation Order (using `new`)

1. Memory is allocated for the object.
2. Instance variables are initialized to their default values.
3. Direct initializations (e.g., `int x = 5;`) are executed in the order they appear in the class.
4. The constructor is called, which may further modify the instance variables.
5. If the class extends another class, the superclass constructor is called *first*; we'll talk more about this in the next chapter about relationships between classes.

# 2.5 Overloading Methods

```java
public int my_method(int something, int something_else){
    return something + something_else;
}

public int my_method(int something){
    return my_method(something, 1);
}
```

# 2.6 Overriding Methods

- `@Override`: informs Java (and readers) that we are overriding an inherited method; NOT necessary

## `equals`

- similar to `__eq__` in python
- default behaviour is `==` (checking for equal object IDs)
- NOT called implicitly by checking identity equality (checking equal object IDs): `==`
- any implementation must obey:
    1. **Symmetry**: For non-null references `a` and `b`, `a.equals(b)` if and only if `b.equals(a)`
    2. **Reflexivity**: `a.equals(a)` must be true
    3. **Transitivity**: If `a.equals(b)` and `b.equals(c)`, then `a.equals(c)`
    
    e.g.,
    
    ```java
    @Override
    public boolean equals(Object obj) {
        if (this == obj){
            return true;
        }
        if (obj == null){
            return false;
        }
        if (this.getClass() != obj.getClass()){
            return false;
        }
    
        MyClass other = (MyClass) obj;  // Here we're casting the type of obj to our class
        // And then we'll want to compare the attributes of this to those of other
        // For example:
        if (this.name != other.name){
            return false;
        } else if (this.something != other.something){
            return false;
        }
        return true;
    }
    ```
    
- would want to override `hashCode` as well
    - The hash code of an object is an integer value (e.g., used by HashMap to decide where to store it) that obeys this property:
        - If two objects are equal (according to the equals method), they have the same hash code.
        - If is not an if-and-only-if: it's fine for two objects with the same hash code *not* to be equal.
    - default `hashCode` is inherited from `Object` class, which is randomly generated

# 2.7 Class (`static`) Methods

```java
public static int population(){
    return MyClass.count;
}
```

- called by prefixing with class name: `MyClass.myMethod()`
    - if an instance (`m1`) of `MyClass` exists, `m1.myMethod()` also works (although not preferred logically/stylistically)
- A class method cannot access an instance variable or call an instance method directly:
    
    e.g., won’t compile:
    
    ```java
    public static int population(){
        return this.some_attribute; // <this> doesn't exist in a class method
    }
    ```
    
    - The only way for a class method to access an instance variable or call an instance method is if a reference to an instance of the class is passed to the method. Through that reference, the instance variables and instance methods of the object are accessible.

# 2.8 keyword <`final`>

- `final`: restricts modification of variables, methods, and classes
    - final *variables* cannot be reassigned after initialization (e.g., for constants)
    - final *object* references cannot be changed/reassigned, BUT object referenced can be mutated (e.g., object attributes can be modified)
    - final *methods* cannot be overriden by subclasses
    - final *classes* cannot be subclassed