# 11-clean-architecture.md

Progress: New
: No
Parent item: Module 3 -- Oct 15-Nov 4 -- Clean Architecture (Module%203%20--%20Oct%2015-Nov%204%20--%20Clean%20Architecture%2026be7be659d980b0aaf7c9535063f6f0.md)
Resources: https://github.com/CSC207-UofT/207-course-notes/blob/master/11-clean-architecture.md

https://github.com/CSC207-2025F-UofT/ca-user-login

https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html

https://youtu.be/Nsjsiz2A9mg?si=jb_vQna71ErLUmCv
More Resources/Practice: screencapture-q-utoronto-ca-courses-394773-quizzes-483173-history-2025-12-17-15_16_54.pdf, CleanArchitectureDiagram_(2).png

# 11.1 The Dependency Rule

![image.png](image%2015.png)

- dependencies in our system must all point inwards — from lower-level policies to higher-level policies
- Dependency Inversion Principle allows for dependencies to point inwards while allowing the flow of information to go from the inside to the outside

# 11.2 The Clean Architecture Engine (CA Engine)

![image.png](image%2016.png)

# 11.3 Clean Architecture by Layer

## Frameworks and Drivers

- `View` — Displays information and reacts to user interaction. The View Will ask a Controller to do something the user wants. The information that the View displays is stored in a ViewModel. When the View Model is updated, the View is alerted and will display the new information to the user.
- `Data Access` — This class reads and writes persistent data to a file or database outside the program. It is again a detail and implements the Data Access Interface specified by the Use Case layer. It will create temporary Entities that the Use Case uses to do its work.

## Interface Adapters

- `Controller` — Converts the raw user data to something useful (for example, a string to a Date object, or a float to a currency value), creates an Input Data object containing that info, and calls a method to start a Use Case, passing in the Input Data.
- `Presenter` — A Presenter class receives information (an Output Data Object) from the Use Case Interactor and turns it into raw strings and numbers to be displayed. The presenter will update the View Model with this information.
- `View Model` — This is a storage class for information the View needs to display. Does the View display the currently logged-in user's name? Then the View Model stores that name. The View accesses the View Model for any information it needs.

## Use Cases

The Use Case layer contains the Use Case Interactors and is responsible for the main actions of the program. This layer incorporates the logic of anything the user of your application can do.

If your program is a calendar app, this layer creates and searches for events. If your program is a messaging app, this is the layer that creates new messages, stores them, retrieves conversations, and any other functionality.

- `Use Case Interactor` — Takes the Input Data and executes the use case, looking up information in the Data Access object when necessary and manipulating Entities. This might create new data that needs to be saved through a Data Access object. When complete, create an Output Data object — the use case result — and pass it to the Presenter.
- `Input Data` — The Controller creates this object and stores input from the user in it. Then this object is passed to the Use Case Interactor. It is designed to be in a format most convenient for the Use Case Interactor to do its job.
- `Output Data` — This class represents the result of executing the Use Case Interactor. The Use Case Interactor creates this object and sends it to the Presenter through the Output Boundary.

### Interfaces

- `Input Boundary` Interface — This is implemented by a Use Case Interactor. Controller classes call the methods in this interface.
- `Output Boundary` Interface — This is implemented by a Presenter class. A Use Case Interactor calls the methods in this interface.
- `Data Access` Interface — This is implemented by a Data Access class. It specifies how the Use Case Interactor will need to access data in order to perform its job.

## Entities

The Entity layer contains the program's "Model" or temporary information storage. The "Enterprise Business Rules" (highest-level policies) are enforced by this layer. For example, the "Enterprise" behind ACORN is the University of Toronto. So if U of T does not let a student enrol in more than 7 course in the same semester, the Student entity class will enforce this rule.

- `Entity` — This is a class that stores information about the building blocks of your program. For example, a car rental app might have classes to represent individual cars (a Car class), individual renters (a Renter class), and so on.

# Misc.

from [https://github.com/CSC207-2025F-UofT/ca-user-login](https://github.com/CSC207-2025F-UofT/ca-user-login)

- UI `State` - “used” by (has-a? property-of?) `ViewModel<T>`
- `ViewModel<T>` -
    - `ViewManagerModel` (extends `ViewModel<String>`) - fires property change `event`s for its listener(s) `ViewManager`; used by (has-a) *presenter* and `ViewManager`
    - use-case specific view models (with use-case specific <state>); used by (use-case specific) *presenter* and  (use-case specific) *view*
- `ViewManager` (implements `PropertyChangeListener`) - listens for property change `event`s in the `ViewManagerModel` and updates which `View` should be visible; used by *presenter*

User input →|→ `View` → `Controller` 
→  [[`InputData` → `InputBoundary`: `Interactor`] → *core program logic processing…*] 
→ [`OutputData` → `OutputBoundary`: `Presenter`]’s ← —`event` — `ViewManagerModel` / (use-case specific) `ViewModel<T>` — `event` —→ `ViewManager` → `View` →|→ UI view