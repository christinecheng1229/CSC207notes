# OOP Explorations Part 1

Progress: New
: No
Parent item: Module 1 -- Sept 17-30 -- Java OOP (Module%201%20--%20Sept%2017-30%20--%20Java%20OOP%2026be7be659d980358a36cfb6580c99bc.md)
Practice: https://q.utoronto.ca/courses/394773/pages/m1-oop-explorations-part-1
More Resources/Practice: JCF-overview.pdf

Review:

Polymorphism in Java:

- each object has more than one type:
    
    `Person x = new Student ();`
    
    Student is the **object type**
    
    Person is the **reference type**
    
    all the other ancestor classes (up to and including `Object`) are also types → lots of layers!
    
- **shadowing** - using something from the reference type
- **overriding** - using something lower than that (maybe from the object type)
- When `Person p = s;` and `s` was a `Student` object, this up-casts `p` to reference type `Person`
- ⭐The only way to get Java to look for a descent version of a method is if the method exists in both the current (parent) and child classes → gets the “updated” instance method
    - otherwise, if the current class doesn’t have the instance method it looks for the method in ancestor classes
    - the other method is to down-cast the current object to use the “updated” method from the child class

Activity 1: Shadowing

```java
class Person {
    public String role = "Person";

    public String getRole() {
        return role;
    }
}

class Student extends Person {
    public String role = "Student";

    public static void main(String[] args) {
        Student s = new Student();
        Person p = s;
        System.out.println(s.role + " " + p.role);
    }
}
```

- What does this main method print?
    
    B. Student Person
    
    - p.role exists → can’t be compile-time or runtime error
    - p references Person, looks in Person class and DOESN’T look down into descendant classes due to shadowing (using refence class)
    - 
    
    [insert image of memory diagram] September 25, 2025 9:00 PM 
    

Activity 2: Overloading

```java
public class Comparer {
    public boolean compare(String a, String b) {
        return a.equalsIgnoreCase(b);
    }

    public boolean compare(Object a, Object b) {
        return a.equals(b);
    }

    public static void main(String[] args) {
        Comparer sc = new Comparer();
        String s1 = "hello";
        String s2 = "HELLO";
        Object o1 = s1;
        Object o2 = s2;
        System.out.println(sc.compare(s1, s2) + " " +
                           sc.compare(o1, o2) + " " +
                           sc.compare(o1, s1));
    }
}
```

- What does this main method print?
    
    A. true false true
    
    - `sc.compare(s1, s2)` - uses most suitable option for inputs (String)
    - `sc.compare(o1, o2)` - uses String version due to overriding; but they are at different addresses so it’s FALSE
    - `sc.compare(o1, s1)` - compares Object type but uses String method version due to overriding

Activity 3: Student Equals

Consider what would happen to ACORN if a student was allowed to change their student number. Consider what happens when a student changes their name.

```java
public class Student {
  private String name;
  private String studentNumber;
  public Student(String name, String stuNum) {
    this.name = name;
    this.studentNumber = stuNum;
  }
}
```

- What  `equals` methods would allow a program containing `Student` to work by similar rules to ACORN? In other words, how can we tell if two `Student` objects both store information about the same real-life person enrolled at U of T?
    
    ```java
    //B.
    public boolean equals(Object o) {
         if (o instanceof Student)
           return o.studentNumber.equals(this.studentNumber);
         else
           return false;
    }
    ```
    
    - definitely need to override default `equals` → rules out D.
    - we don’t want same name to mean they are the same student → rules out A. and C.

Activity 4: Buggy Equals 1

```java
class Student {
    String name;
    String studentNumber;

    public Student(String name, String studentNumber) {
        this.name = name;
        this.studentNumber = studentNumber;
    }

    public boolean equals(Student s) {
        return studentNumber.equals(s.studentNumber);
    }

    public static void main(String[] args) {
        Student s1 = new Student("Alice", "123");
        Student s2 = new Student("Alice", "123");
        Object o2 = s2;
        System.out.println(s1.equals(s2) + " " + s1.equals(o2));
    }
}
```

- What does this main method print?
    
    D. true false
    
    - 1st s1 calls student equals → TRUE
    - 2nd s1 calls Object equals because o2 has Object reference type and Student’s equals doesn’t have the same method signature as Object’s equals (takes in Student instead of Object) → overloading equals instead of overriding ⇒ uses Object’s equals (checks object address) → FALSE

Activity 5: Buggy Equals 2

```java
class Student {
    String name;
    String studentNumber;

    public Student(String name, String studentNumber) {
        this.name = name;
        this.studentNumber = studentNumber;
    }

    public boolean equals(Student s) {
        return studentNumber.equals(s.studentNumber);
    }

    public static void main(String[] args) {
        Student s1 = new Student("Alice", "123");
        Student s2 = new Student("Alice", "123");
        Object o1 = s1;
        System.out.println(o1.equals(s2) + " " + s1.equals(s2));
    }
}
```

- What does this main method print?
    
    C. false true
    
    - o1 uses Object equals
    - s1 uses Student equals

Activity 6: Buggy Equals 3

```java
class Student {
    String name;
    String studentNumber;

    public Student(String name, String studentNumber) {
        this.name = name;
        this.studentNumber = studentNumber;
    }

    public boolean equals(Student s) {
        return studentNumber.equals(s.studentNumber);
    }

    public static void main(String[] args) {
        Student s1 = new Student("Alice", "123");
        Student s2 = new Student("Alice", "123");
        Set<Student> set = new HashSet<>();
        set.add(s1);
        System.out.println(set.contains(s2));
    }
}
```

- What does this main method print?
    
    B. false
    
    - Hashmap.contains(e) uses equals of set and s2 ⇒ compares address → FALSE

Activity 7: Vehicles Go in Different Ways

```java
public class Vehicle {
  public void go() {
    System.out.println("Drive or Ride");
  }
}

public class Bicycle extends Vehicle {
  public void go() {
    System.out.println("Ride");
  }

  public void go(int distance) {
    System.out.println("Ride for " + distance + " km");
  }
}
```

- What will be the result of running the following code snippet:
`Vehicle obj1 = new Bicycle();
obj1.go(3);`
    
    D. Compile-time error
    
    - didn’t case `obj1` as a Bicycle, thus it tries to use `Vehicle`’s go which doesn’t take arguments