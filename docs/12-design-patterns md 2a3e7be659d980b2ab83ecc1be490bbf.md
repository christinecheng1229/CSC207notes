# 12-design-patterns.md

Progress: New
: No
Parent item: Module 4 -- Nov 5-18 -- Design Patterns (Module%204%20--%20Nov%205-18%20--%20Design%20Patterns%2026be7be659d980ee9ba1ff749a329e87.md)
Resources: https://github.com/CSC207-UofT/207-course-notes/blob/master/12-design-patterns.md

https://github.com/CSC207-UofT/207-course-notes/tree/master/code/design_patterns

https://q.utoronto.ca/courses/394773/pages/m4-builder-examples

https://refactoring.guru/design-patterns

https://sourcemaking.com/design_patterns
More Resources/Practice: DesignPatterns.pdf, screencapture-q-utoronto-ca-courses-394773-quizzes-485098-history-2025-12-17-15_57_09.pdf, screencapture-q-utoronto-ca-courses-394773-quizzes-484945-history-2025-12-17-16_06_32.pdf

# 12.1 What is a Design Pattern

Descriptions of popular solutions to commonly-experienced programming problems

- **anti-pattern**: If a less convenient solution has been implemented instead
    - → can (and should) improve design by refactoring to implement a design pattern instead
- describes code *structure*
- NOT specific to any programming language → UML diagrams are a good way to describe structure of design patterns
- Analogy: In math, *theorems* are proven results derived from *axioms*. In software, *design patterns* are established solutions derived from applying design principles to common problems. These patterns are intended to be more practically applicable and less abstract than their underlying principles.

# 12.2 Creational Patterns

- Focus: creation of objects → aim to avoid tight coupling, excessive use of constructors, and inflexible instantiation logic that introduces hard dependencies
- addresses the question of where `new MyClass(...)` calls should occur in our code, and how the created objects are linked together: ”who is responsible for creating each object in our system?”

## 12.2.1 Factory Pattern

**Problem:** You need to create objects that are all subclasses or implementing classes of the same abstraction, but you don’t want your code to depend on the exact class names or how they’re built.

**Solution:** Use a special “factory” object or method that decides which class to create and returns a ready-to-use instance.

There are several variations of the Factory pattern, but they all share the same basic idea.

1. The first variation is the **Simple Factory** pattern, which *uses a (usually static) method to create objects based on input parameters*. It can produce different concrete types that share a common interface or superclass.
    
    Example: requires `Shape` objects, but doesn't need to know if they are rectangles, circles, triangles, or any other shape that you might want to include in the future
    
    ```java
    public class ShapeFactory { 
        public Shape getShape(String shapeType) {
            switch(shapeType) {
                case "Rectangle": 
                    return new Rectangle(); 
                case "Circle": 
                    return new Circle(); 
                case "Square": 
                    return new Square();
                default:
                    throw new IllegalArgumentException(
                            "Wrong shape type: " + shapeType
                    );
            }
        }
    }
    
    // Client C
    :
    ShapeFactory shapeFactory = new ShapeFactory();
    Shape shape = shapeFactory.getShape(userInput);
    // if getShape method is static:
    Shape shape = ShapeFactory.getShape(userInput);
    ```
    
    NOTE: When adding a new shape type, the `getShape` method needs to be modified, since the conditional logic is within the method
    
2. The second variation is the **Factory Method** pattern, which *uses inheritance to allow subclasses to decide which concrete class to instantiate*.
    - similar to Abstract Factory pattern except that the roles of the Client and Factory classes are combined. (Effective Java by Joshua Bloch has a section devoted to Static Factory Methods, which are also similar to the Factory Method pattern.)
3. The third variation is the **Abstract Factory** pattern, which *uses composition to delegate the instantiation logic to another object*. This creates a family of one or more related objects.
    
    ![image.png](image%2017.png)
    
    (same) Example: requires `Shape` objects, but doesn't need to know if they are rectangles, circles, triangles, or any other shape that you might want to include in the future
    
    ```java
    public abstract class ShapeFactory {
        public abstract Shape getShape();
    }
    
    public class RectangleFactory extends ShapeFactory {
        public Shape getShape() {
            return new Rectangle();
        }
    }
    
    public class CircleFactory extends ShapeFactory {
        public Shape getShape() {
            return new Circle();
        }
    }
    
    public class SquareFactory extends ShapeFactory {
        public Shape getShape() {
            return new Square();
        }
    }
    
    // Client code:
    public class Main {
        public static void main(String[] args) {
            ShapeFactory factory = new CircleFactory();  // could be chosen based on user input
            // Factory choice (conditional logic) is outside of any methods
            Shape shape = factory.getShape();
            // do something with the shape...
        }
    }
    ```
    
    NOTE: When adding a new shape type, the `getShape` method needs to be modified, since the conditional logic is within the method
    

![The client uses a provided factory to create instances of the product that it needs for its work.](image%2018.png)

The client uses a provided factory to create instances of the product that it needs for its work.

| **Aspect** | **Simple Factory** | **Abstract Factory** |
| --- | --- | --- |
| Creation logic | All in one class | Distributed across subclasses |
| Adding new types | Add a new if-statement (modify existing code) | Add a new factory subclass (extend existing code) |
| Client usage | Client specifies type through String parameter | Client chooses the factory |

## 12.2.2 Builder Pattern

**Problem:** Creating a complex object with many parts or options makes your code messy and hard to read.

**Solution:** Use a step-by-step “builder” that assembles the object piece by piece, then gives you the finished product.

This follows a pattern:

- Create a "builder" object
- Add parts to it step-by-step.
- Get the final product.

![image.png](image%2019.png)

Example: `Hatchimal toString` method

```java
    public String toString() {
        return new StringBuilder() // "builder" object (in this case, a StringBuilder)
					       // step-by-step adding parts (Here, by calling append() multiple times)
                 .append("Hatchimal{")
                 .append("name='").append(name).append('\'')
                 .append(", rarity=").append(rarity)
                 .append('}')
                 .toString(); // get final product (Here, by calling the builder's toString() method)
        }
```

Example: `Okhttp` code we used to make API calls

```java
Request request = new Request.Builder()
                .url(String.format("%s/grade?username=%s", API_URL, username))
                .addHeader(TOKEN, getAPIToken())
                .addHeader(CONTENT_TYPE, APPLICATION_JSON)
                .build();
```

[IntelliJ feature](https://www.jetbrains.com/help/idea/replace-constructor-with-builder.html)

# 12.3 Behavioural Patterns

- Focus: how objects interact and communicate
- addresses the question of how responsibilities and behaviours are distributed across the objects in our system, and how those objects communicate to get things done

## 12.3.1 Strategy Pattern

**Problem:** You have several algorithms to do the same task, and you want to switch between them easily.

**Solution:** Implement each algorithm in its own class and make them interchangeable, so that you can change the algorithm without changing the code that uses it.

- Setting which Strategy to use is often done either through the constructor (like in the example) or a setter (like in the UML class diagram).
- Strategies often correspond to code that may be useful in multiple contexts.

![image.png](image%2020.png)

Example:  a class called `Map` that requires a `getDirections` method, which should return a different `String` depending on whether the directions are for driving or public transit.

```java
public class Map {

	private DirectionGenerator dg;

	public Map(DirectionGenerator dg) {
	    this.dg = dg;
	  }

	public getDirections() {
	    dg.getDirections();
	   }
}
```

We call the `DirectionGenerator` interface the Strategy and have classes `DrivingDirections` and `TransitDirections` implement it. When the `Map` class is instantiated, it is given an object implementing the Strategy.

- Context = `Map`
- Strategy interface = `DirectionGenerator`
- Concrete Strategies = `DrivingDirections`, `TransitDirections`

## 12.3.2 Observer Pattern

**Problem:** Multiple parts of your program need to react when an object changes, but you don’t want tight coupling between those parts and the object being observed.

**Solution:** Define a one-to-many relationship: when the observed object changes, all related objects get notified so that they can respond. The observed object doesn't need to know anything about the specifics of the objects observing it.

“separates the cause from its effect”, but not just any cause — more specifically a *property* change that results in a different result

![An `Observable`'s job is to notify all its `Observer`s when it changes](image%2021.png)

An `Observable`'s job is to notify all its `Observer`s when it changes

- In Java, this is usually accomplished by having the `Observable` use a `java.beans.PropertyChangeSupport` object, which manages a list of `PropertyChangeListener` objects (the `Observers`) so that you don't have to write the code that manages the list of `Observers` yourself.
- When the `Observable`'s state changes, it calls the `firePropertyChange` method of its `PropertyChangeSupport` object, which in turn calls the `propertyChange` method of each `PropertyChangeListener`.

Example: Clean Architecture `View` and `ViewModel`

- each `View` will observe its `ViewModel` → When the data in the `ViewModel` changes, the corresponding `View` needs to update itself to reflect the new data
- `ActionListener` objects that we attach to `JButton` components. When the button is clicked (event), the listener’s `actionPerformed` method is called (reaction).

```java
public class LoginView extends JPanel implements ActionListener, PropertyChangeListener {
    
    // Other methods not shown.
    
    public void propertyChange(PropertyChangeEvent evt){
        // React to the change event.
        final LoginState state = (LoginState) evt.getNewValue();
        setFields(state);  // This method will update the View's fields based on the data in the new state.
    }
}

public class ViewModel<T> {
    private final PropertyChangeSupport support = new PropertyChangeSupport(this);
    
    public void addPropertyChangeListener(PropertyChangeListener listener) {
        this.support.addPropertyChangeListener(listener);
    }

    // This gets called by the Presenter when it is done updating the ViewModel. (Note that this delegates to a helper method.
    public void firePropertyChanged() {
        this.support.firePropertyChange("state", null, this.state);
    }

    public void firePropertyChanged(String propertyName) {
        this.support.firePropertyChange(propertyName, null, this.state);
    }
    
}
```

# 12.4 Structural Patterns

- Focus: how classes and objects are combined to form larger systems; how components are connected and organized

## 12.4.1 Façade Pattern

**Problem:** A subsystem exposes many classes and operations to clients, forcing them to deal with unnecessary complexity.

**Solution:** Create a simple client-facing class (the *façade*) that provides methods for common tasks while hiding the subsystem's complex details.

“hides away the methods and logic”

![image.png](image%2022.png)

Side note: When constructing a façade, a creational pattern such as *Builder* can be useful for assembling its internal components in a systematic way.

Example: `EmployeeFacade` class

Contains variables of type:
`EmployeeCalculator` that is responsibility for calculating the employee's pay,
`EmployeeReporter` that reports the employee's hours, and
`EmployeeSaver` that sends the updated employee information to a database.

```java
public class EmployeeFacade {

    private PayCalculator payCalculator;
    private HourReporter hourReporter;
    private EmployeeSaver employeeSaver;
    
    public float calculatePay() {
       return this.payCalculator.calculatePay();  // Notice the 1-line delegation 
    }
    
    // The other methods go here and are structured the same way. They delegate to the appropriate object.
}
```

## 12.4.2 Adapter Pattern

**Problem:** Two components can’t work together because their interfaces don’t match. This often happens when you need to reuse an existing class that was designed for a different context.

**Solution:** Introduce an *adapter* — a class that translates between the expected interface and the existing one. The adapter exposes the interface your client code expects and internally forwards calls to the legacy class, converting inputs and outputs as needed. This can be done by:

- **Delegation**: The adapter holds a reference to the legacy class and delegates work to it.
- examples from CA engine: interface adapters e.g., controller adapts input for use case interactor

![image.png](image%2023.png)

- **Inheritance**: The adapter extends the legacy class and adds code to be consistent with the expected interface.

![image.png](image%2024.png)

Example: `Ticket` class → `MovieTicket` class

`Ticket`: originally written for a lottery program. If the number on your ticket matches a randomly selected number, you win.

`MovieTicket`: class in a program that sells tickets for a movie theatre. The `Ticket`class doesn’t support seat numbers, so we need to adapt it.

```java
// With Delegation
public class MovieTicket {

    private Ticket ticket = new Ticket(); // the class being adapted
    private String seatNumber;

    public MovieTicket(String seatNumber) {
        this.seatNumber = seatNumber;
    }

    public void sellTicket() {
        // delegate work to the Ticket class and add extra behavior
        ticket.sell();
        System.out.println("Seat: " + seatNumber);
    }
}

// With Inheritance
public class MovieTicket extends Ticket {

    private String seatNumber;

    public MovieTicket(String seatNumber) {
        super(); // initialize the Ticket part
        this.seatNumber = seatNumber;
    }
    
    public void sellTicket() {
        // reuse parent's sell method and add extra behavior
        super.sell();
        System.out.println("Seat: " + seatNumber);
    }
}
```

# 12.5 Summary

| **Category of Pattern** | **Focus** | **Key Question** | **Representative Patterns** |
| --- | --- | --- | --- |
| **Creational** | Object creation | Who is responsible for creating each object in our system? | Factory, Builder |
| **Behavioral** | Object interaction and communication | How are responsibilities and behaviors distributed across objects, and how do objects communicate to get things done? | Strategy, Observer |
| **Structural** | Object and class organization | How can we connect and organize objects to work together? | Adapter, Façade |