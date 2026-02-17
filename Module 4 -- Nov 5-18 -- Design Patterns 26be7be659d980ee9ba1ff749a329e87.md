# Module 4 -- Nov 5-18 -- Design Patterns

Progress: New
: No
Resources: • The Clean Architecture book talks about several patterns in passing, but this topic isn't the focus of the book:
    ◦ Chapter 11: DIP talks about the Abstract Factory pattern near the end.
    ◦ Chapter 23: Presenters and Humble Objects talks about the Humble Object pattern which you may find interesting as it relates to how the Clean Architecture is designed to be testable.
    ◦ Façades and the Strategy pattern are briefly discussed at the end of Chapter 24: Partial Boundaries.
• Head First Design Patterns is a highly recommended first book on design patterns.
More Resources/Practice: PropertyChangeDocumentation.pdf
Sub-item: 12-design-patterns.md (12-design-patterns%20md%202a3e7be659d980b2ab83ecc1be490bbf.md), Design Patterns 1 (Design%20Patterns%201%202a4e7be659d980d38e1dd434653e6bf9.md), 13-refactoring-techniques.md (13-refactoring-techniques%20md%202a3e7be659d9806f81aef8f492bad33a.md), Refactoring the Observer Anti-Pattern (Refactoring%20the%20Observer%20Anti-Pattern%202aae7be659d980738723ef9f15aa10f4.md), Design Patterns 2 (Design%20Patterns%202%202cce7be659d980e3a636cbf901a4446a.md), Identifying New Design Patterns (Identifying%20New%20Design%20Patterns%202abe7be659d98083874fdba0e7917882.md)

By the end of this module, you will be able to:

- Identify and implement design patterns, including:
    - Creational patterns: Builder, Factory
    - Behavioural patterns: Strategy, Observer
    - Structure patterns: Façade, Adapter
- Explain what an anti-pattern is and identify examples in code
- Apply various refactoring techniques in IntelliJ (Extract Method, Change Method Declaration, Encapsulate Fields, Split Loop, Slide Statements, Replace Constructor with Builder, Replace Constructor with Factory Method)
- Plan code by creating GitHub issues and a README, and then implement the code
- Given a Use Case, create a Use Case Interactor for each user-generated event (like a button click). Each interactor requires that you write code to do the following:
    - Write a listener method to handle the event
    - Invoke a Controller
    - Invoke an Interactor
    - Request Entities from DAOs
    - Invoke the Presenter
    - Update the ViewModel
    - Apply the Observer pattern to have the View react to the update in the ViewModel