# Unit Test for a Use Case Interactor

Progress: New
: No
Parent item: Module 3 -- Oct 15-Nov 4 -- Clean Architecture (Module%203%20--%20Oct%2015-Nov%204%20--%20Clean%20Architecture%2026be7be659d980b0aaf7c9535063f6f0.md)
Resources: https://github.com/CSC207-2025F-UofT/ca-lab (/w examples of testing use cases)
    ◦ https://github.com/CSC207-2025F-UofT/ca-lab/blob/main/src/test/java/use_case/login/LoginInteractorTest.java
More Resources/Practice: testing_use_cases.pdf

# Part 1

- Activity 1
    - E - all of them
        
        🌟Great summary of what each part of the CA engine does:
        
        i. The most important class is NewAccountInteractor. All the other New* interfaces and classes exist
        
        purely to support the interactor.
        
        ii. The Input Boundary exists so that the controller knows how to invoke the interactor.
        
        iii. The Input Data class exists to package up the data the interactor needs to do its work. The Controller
        
        instantiates it.
        
        iv. The NewAccountDataAccessInterface is implemented by a Data Access Object (DAO). This interface exists
        
        so that the DAO knows what methods the interactor will use to request Entities from the data layer.
        
        v. The Output Boundary exists so that the interactor knows what methods it can call to deliver the output data
        
        to the UI layer. A Presenter implements this interface.
        
        vi. The Output Data class exists to package up the data the interactor produces to send to the Presenter. The
        
        interactor instantiates the Output Data.
        

# Part 2

- Activity 1
    
    C The username of the account to check
    
    - A - if the account creation was know, likely the user already knows whether account is new; unnecessary for this usecase
    - B - the input boundary is implemented by the interactor → it doesn’t not except to recieve an instance of itself
    - D - may be used to create a new account (Entity) along with DataAccessInterface, but doesn’t except to recieve it
- Activity 2
    
    D An object containing all the information that needs to be updated in the UI.
    
    - A - is a part of A, and may be represented by a String or boolean, but the front-view moreso needs to know whether this means a success (view) or fail view (ie., main flow vs alternate flow)
- Activity 3
    
    A, B
    
    - D - terrible idea since you are changing the interface
    - C - InputData objects are the disposable objects that stores input data to be used by the interactor, but is not input boudary’s execute