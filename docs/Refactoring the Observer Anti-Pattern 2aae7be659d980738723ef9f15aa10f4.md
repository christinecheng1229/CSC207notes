# Refactoring the Observer Anti-Pattern

Progress: New
: No
Parent item: Module 4 -- Nov 5-18 -- Design Patterns (Module%204%20--%20Nov%205-18%20--%20Design%20Patterns%2026be7be659d980ee9ba1ff749a329e87.md)
Resources: https://github.com/CSC207-UofT/207-course-notes/tree/master/code/design_patterns/behavioural/observer

https://refactoring.guru/refactoring/techniques

https://refactoring.guru/refactoring/smells
Practice: https://q.utoronto.ca/courses/394773/pages/m4-refactoring-the-observer-anti-pattern

“smelly code”: things in the code that when fixed now, saves significant time/fixing later

**refactoring**: changing the code without changing its *functionality*

→ refactor to fix problems with  the *design* (not functionality, or compilation, etc.)

Refactoring techniques:

Extract Method

- improves readability and makes it easier to alter a specific step of the longer method
- increases length of class

Change Method Declaration

Encapsulate Fields

- beyond setting  a public instance variable to private, you can also take it one step further by placing all these variable in a separate class and creating an instance of this object in the original class

Split Loop

- lengthens the class, increase amount of methods/runtime
- easier for someone to edit the content of a specific component/function independently from other parts of the course (open for extension-closed for modification)

Slide Statements

Replace Constructor with Builder

Replace Constructor with Factory Method

# Examples

![image.png](image%2025.png)

- (^)
    
    C. Encapsulate Fields
    
    ![image.png](image%2026.png)
    

![image.png](image%2027.png)

- (^)
    
    D Replace Constructor with Builder
    
    ![image.png](image%2028.png)
    
    - could also argue to use a factory method and have cheese and peperoni pizzas be sub-classes of pizza (although that’s not exactly what factory does)

![image.png](image%2029.png)

- (^)
    
    Multiple things to be done (best in the following order):
    
    D Split Loop → E Slide Statements → A Extract Method (extract code from `main()` into a separate class since it’s more difficult to test a static method, then create an instance of that class to execute the code)
    

# `Parcel` Anti-pattern

[https://github.com/CSC207-UofT/207-course-notes/tree/master/code/design_patterns/behavioural/observer/without_observer](https://github.com/CSC207-UofT/207-course-notes/tree/master/code/design_patterns/behavioural/observer/without_observer)

![image.png](image%2030.png)

`Parcel` is directly dependant on `Company` and `Customer`, which are dependencies we don’t want

- the `Parcel` class also directly stores instance of its observers → only a single instance of both object types can exist ← less flexibility
- the observer objects are directly made aware of the change of state happening in `locationChanged()`, which is something we don’t want
- Q1
    
    D. Two of the above reasons. (B and D)
    
    - A is a fact that’s true to the observer patten specifically in Java, but not part of the anti-pattern problem
- Q2
    
    **B.** "Change Method Declaration" so the `addCompany` and `addCustomer` methods are replaced with `addListener` which takes in a variable of type `PropertyChangeListener`. We would also have to ensure that the `Company` and `Customer` classes implement a `PropertyChangeListener` interface.
    
    - interface allows you to add any additional types of objects as one wishes
- Q3
    
    C. Encapsulate Fields
    
    - We’ve hidden the variables into the `PropertyChangeSupport` variable
    - If instead of `Parcel`, we were doing this for the `main` method, we can argue for **D.** replacing constructor with builder
- Q4
    
    **B.** Delegate to `PropertyChangeSupport.firePropertyChange`
    
    - `firePropertyChange` tells the `PropertyChangeSupport` to tell the observers
    
    **C.** Delete the `locationChanged` method
    
- Q5
    
    **A.** It is required by the `PropertyChangeListener` interface.
    
- Q6
    
    **D.** `Main`
    
    - use `addObserver` instead of `setCustomer`/`setCompany`

At the end:

![image.png](image%2031.png)

[https://github.com/CSC207-UofT/207-course-notes/tree/master/code/design_patterns/behavioural/observer/with_observer](https://github.com/CSC207-UofT/207-course-notes/tree/master/code/design_patterns/behavioural/observer/with_observer)