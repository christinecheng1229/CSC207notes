# OOP Explorations 2

Progress: New
: No
Parent item: Module 2 -- Oct 1-14 -- Design Principles (Module%202%20--%20Oct%201-14%20--%20Design%20Principles%2026be7be659d980fea17ce010271854ea.md)
Resources: https://github.com/jcal13/area-calculator
Practice: https://q.utoronto.ca/courses/394773/pages/m2-oop-explorations-part-2
More Resources/Practice: ShapeCalculatorExample.pdf

Consider the Person and Student classes below. Assume they are part of a larger program. 

![image.png](image%202.png)

- What can we conclude about the program?
    
    D. This program does not allow you to change someone’s student number.
    
    - no setter for the private variable → “Defensive Programming”
- If our goal is to write code that is self-explanatory to other members of our team, what can we learn from the above example?
    
    B. Only include "setters" for variables whose values can be changed without breaking the program.
    
- The Liskov Substitution Principle says that it should be possible to replace an object of a super type with an object of its subtype without breaking the program. In order for this to be true, which is required?
    
    A. Student should be a subclass of Person
    
    If the reverse was true, you are forcing all Person objects to have a student number, even if they don’t actually have such a value to store
    

Consider the Rectangle and AreaCalculator classes below. They are part of a larger program that draws shapes on the screen and calculates the total area of all shapes being displayed.

![image.png](image%203.png)

- Our current goal is to add a Circle class to this program and other classes like Triangle, Oval, Trapezoid, etc. Which design would require less work to add these classes in the future?
    
    D. Create a Shape class. Have Rectangle and Circle extend Shape and store an array of Shape objects in the AreaCalculator.
    
- Consider this declaration:
`Shape s1 = new Rectangle();`
We want to store s1 and other objects in an array of Shape objects. What should Shape be?
    
    A. Shape should be an abstract class.
    
    C. Shape should be an interface.
    
    can also be true since we don’t need to inherit anything from Shape, just need the program to be able to treat it as a shape → thus gives “shape function” → interface!
    

![image.png](image%204.png)

- The area of a rectangle is length * width. The area of a circle is pi * radius^2. Other Shape subclasses will have other area formulas. Consider the updated UML diagram of shape-related classes. Our current goal is to add more subclasses of Shape without having to change the code in the AreaCalculator. What is required for this to happen?
    
    C. Shape should contain an abstract `area` method so that Rectangle and Circle have to implement it.
    
    NOTE: if you find yourself needing to do`instanceOf()` within a method, likely the method is in the wrong class and it should be placed in a class that knows its own identity and can perform the method based on that information
    
- The new design from question 5 is an example of which principle(s)?
    
    B. All three
    
    (i) Single Responsibility Principle:
    
    Each class should have at most one source of potential change.
    For example, the only reason to change the Rectangle class is if the UI designing decides to change what information is required to draw a rectangle on the screen.
    
    - if someone wants to change how to calculate area of a circle, then they only need to care about the circle class, not the shape class since shape is abstract
    
    (ii) Open/Closed Principle
    
    It should be possible to add new feature to a program ("open for extension"), without having to change the existing code ("closed for modification").
    
    (iii) Dependency Inversion Principle
    
    When possible, a class should depend on an abstraction, not a detail. This can mean it is better to depend on something further from the UI or it could mean depending on something higher in the inheritance hierarchy.