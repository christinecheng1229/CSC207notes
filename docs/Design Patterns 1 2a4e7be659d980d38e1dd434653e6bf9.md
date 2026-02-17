# Design Patterns 1

Progress: New
: No
Parent item: Module 4 -- Nov 5-18 -- Design Patterns (Module%204%20--%20Nov%205-18%20--%20Design%20Patterns%2026be7be659d980ee9ba1ff749a329e87.md)
Practice: https://q.utoronto.ca/courses/394773/pages/m4-design-patterns-1

- Activity 1
    
    **C.** Adapter
    
    you are turning information from one class, to be usable by another class
    
    - Façade - shouldn’t have any logic; the `Controller` *may* be a Façade, but the `Data Access Object` is pretty much never a Façade
    - Builder - neither controller nor DAO involves any constructors, which are characteristic of Builder (and Factory) pattern
    - **D.** Something else
        - Could argue that DAO implemments Strategy pattern, since it is a strategy (amongst potential others) of storing data (e.g., you could have a different DAO to store data in a different format)
- Activity 2
    
    **B.** Observer
    
    - Façade - no logic in the class: delegates work to other classes
    - Strategy - multiple different classes (strategies) implementing `PostageCalculator` and `DeliveryMethod`
    - **D.** Actually, it implements all of Façade, Observer, and Strategy.
        - could argue that getPostage() separates the caller (Parcel class) from the actual location of the logic/caller
- Activity 3
    
    **A.** It is possible to add new subclasses of Shape or change the constructor of, say, the Rectangle class, without changing any other class outside of the ShapeFactory.
    
    - for example, to add a new shape type, just need to implement the shape class itself and add a few lines to the factory
    - This code is NOT easy to refactor into the Builder pattern
        - Factory creates one object, Builder can do multiple things/build multiple parts and returns
        - Factory can create an object of one class (constructor type) and return another type (declaration type), builder returns object type that matches the object created/built