# 10-introduction-to-layered-architectures.md

Progress: New
: No
Parent item: Module 3 -- Oct 15-Nov 4 -- Clean Architecture (Module%203%20--%20Oct%2015-Nov%204%20--%20Clean%20Architecture%2026be7be659d980b0aaf7c9535063f6f0.md)
Resources: https://github.com/CSC207-UofT/207-course-notes/blob/master/10-introduction-to-layered-architectures.md

🌟Low coupling, high cohesion

**policies** — rules that govern how inputs are transformed into outputs

- ie.,  how data needs to look at different points in a system
- a policy provides a set of *invariants*, *preconditions*, and *postconditions*

Policies exist at different **levels**:

- **High-level policies** are far from input/output and represent the core logic of the application.
- **Low-level policies** are close to input/output and deal with things like UI interactions, file access, or network communication.

Goal: keep high-level policies independent of low-level ones ⇒  improves testability, reduces coupling, and makes the system easier to reason about

# 10.1 Event-driven programming: a network of objects

**events**: user actions (e.g., clicks, keystrokes, etc.)

`event_listener_method(event) {// calls other methods to handle event}` ⇒ chain of method calls across objects:

- call stack of method calls (event listening usually at bottom)
- heap of objects involved

# 10.2 Layers and coupling

A **model** is how you choose to represent the data in the program, such as creating a `Book` class so that you can use `Book` objects to represent the current state of the system. These kinds of objects are often called **entities**.

⭐models should *not* have dependencies on the UI or database layer (shouldn’t mention any classes definied in those layers)

Architecture patterns:

- model view controller (MVC)
- model view presenter (MVP)
- model view viewmodel (MVVM)
- ports and adapters architecture
- onion architecture
- hexagonal architecture
- clean architecture

→ they all contain event listener method in the UI layer

# 10.3 **Model View Controller (MVC)**

![[https://subscription.packtpub.com/book/programming/9781788624060/7/ch07lvl1sec56/the-model-view-controller-pattern](https://subscription.packtpub.com/book/programming/9781788624060/7/ch07lvl1sec56/the-model-view-controller-pattern)](image%2013.png)

[https://subscription.packtpub.com/book/programming/9781788624060/7/ch07lvl1sec56/the-model-view-controller-pattern](https://subscription.packtpub.com/book/programming/9781788624060/7/ch07lvl1sec56/the-model-view-controller-pattern)

- The user interacts with the View, which creates an event
- The Java system calls a listener method in a View object
- The View immediately calls a method in the Controller to handle the event
- The Controller manipulates the Model
- The Model fetches any necessary data from the database
- The Model calls a method in a View object to let it know that there's been an update
- The Controller decides which screen to display
- The View calls getter methods on the Model and updates the UI

*NOTE*: the tight coupling between the View and the Model

# 10.4 **Model View Presenter (MVP)**

![image.png](image%2014.png)

- The user interacts with the View, which creates an event
- The Java system calls a listener method in a View object
- The View immediately calls a method in the Presenter to handle the event
- The Presenter manipulates the Model
- The Model fetches any necessary data from the database
- The Model calls a method in a Presenter object to let it know that there's been an update
- The Presenter calls methods in the View to update the user interface

# 10.5 tbc

October 17, 2025 9:00 AM