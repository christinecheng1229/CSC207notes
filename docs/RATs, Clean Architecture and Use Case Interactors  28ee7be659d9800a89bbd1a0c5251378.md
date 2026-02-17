# RATs, Clean Architecture and Use Case Interactors Activities

Progress: New
: No
Parent item: Module 3 -- Oct 15-Nov 4 -- Clean Architecture (Module%203%20--%20Oct%2015-Nov%204%20--%20Clean%20Architecture%2026be7be659d980b0aaf7c9535063f6f0.md)
Practice: https://q.utoronto.ca/courses/394773/pages/m3-clean-architecture-part-1 | https://q.utoronto.ca/courses/394773/pages/m3-use-case-interactors
More Resources/Practice: screencapture-q-utoronto-ca-courses-394773-quizzes-482244-history-2025-12-17-15_20_52.pdf

# RAT

- Q1
- Q2
    
    
    - has rules so it can either be in the Entity or Use Case Adapter layer, but is less of an action (use case) → Entity layer
- Q3
    - Data Access since we are storing information *outside* the program
- Q4

# Clean Architecture Activity

![image.png](image%2012.png)

- Q1
    
    B. Use Case Interactor
    
    - after completing the key logic of the particular use case, it will aim to write the output somewhere (via `Data Access` Interface)
- Q2
    
    event listener method in `View` and `Controller` sends information from front end to back end to the `Input Data` data store
    
    C. In an Input Data object
    
    - NOTE: each unique use case should get its own set of `Use Case` layer components (Input Data, Use Case Interactor, Data Access Interface, etc.), and likely at least one corresponding controller
- Q3
    
    C. To transfer results from the Use Case Interactor to the Presenter
    
- Q4
    
    A. After being idle for a set period of time, the user has to log in again to access ACORN.
    
    - since Quercus and ACORN have different idle times (and both applications are under the same UofT enterprise), rule A is an *application* business rule
- Q5
    
    
- Q6

# **Use Case Interactors Activity**

- Part 1:
    - Use Case Interactors don’t call Controller methods → eliminate all those
    
    C. Check if the user already has an account.
    
    D. Check if the two passwords in the SignupInputData match each other.
    
    E. Warn the Presenter if the passwords do not match.
    
    not directly, but we *are* going through the Output Boundary Interface to ensure the failure messaging is given to user
    
    ~~F. Warn the user if the passwords do not match.~~
    
    User Case Interactor shouldn’t be interacting that far to user
    
    H. Warn the Data Access Object if the passwords do not match.
    
    potentially some type of logging could be wanted (e.g., of log-in/password change history log) (— up to developer’s discretion!), which would be done via the Data Access Interface implemented by a Data Access Object
    
    I. Send a warning to the same place as the other warning if the user already has an account.
    
    ~~K. Ask the Presenter if the two passwords contain enough letters, numbers, etc.~~
    
    not Presenter’s job — it’s responsible for formatting data from backend to be displayed in the front end
    
    L. Check directly if the two passwords contain enough letters, numbers, etc.
    
    yes, probably an application business rule!
    
    M. Create a new User or Account object for the new user.
    
    calls Entities constructor to create the appropriate object(s)
    
    ~~N. Send the new User or Account object directly to a database outside the program.~~
    
    job of the data access object
    
    O. Send the new User or Account object to a Data Access Object for storage in the persistence layer.
    
    P. Save the new User or Account object with all the other User or Account objects in the Entity layer.
    
    Q. Create a SignupOutputData object.
    
    ~~R. Pass the SignupOutputData object to the Data Access Object.~~
    
    the output object is just for front end, doesn’t need to be stored in the database
    
    S. Pass the SignupOutputData object to the Presenter.
    
    via Output Boundary Interface
    
    ~~T. Pass the SignupOutputData object to the Controller.~~
    
    wrong direction of usage (arrow) and this isn’t the controller’s job
    
    ~~U. Save the SignupOutputData object with all the other Output Objects in the Entity layer.~~
    
    output data is an entity, but is temporary (just needed for output)
    
- Part 2:
- Part 3:

Note:

- technically if the program doesn’t have enterprise business rules, entities aren’t needed
    - I.e., if you only have application business rules, you’ll only need the use case interactors (and its dependencies, etc.) data access, etc.
    - e.g., if UofT doesn’t allow student to graduate with overdue books (an enterprise business rule), then the overdue book status is updated by library application(s), but needs to be check-able by other applications ⇒ student needs to be an entity