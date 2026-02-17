# 09-design-principles.md

Progress: New
: No
Parent item: Module 2 -- Oct 1-14 -- Design Principles (Module%202%20--%20Oct%201-14%20--%20Design%20Principles%2026be7be659d980fea17ce010271854ea.md)
Resources: https://github.com/CSC207-UofT/207-course-notes/blob/master/09-design-principles.md

https://blog.cleancoder.com/uncle-bob/2020/10/18/Solid-Relevance.html

https://blog.cleancoder.com/uncle-bob/2014/05/08/SingleReponsibilityPrinciple.html

https://blog.cleancoder.com/uncle-bob/2014/05/12/TheOpenClosedPrinciple.html

https://blog.cleancoder.com/uncle-bob/2013/03/08/AnOpenAndClosedCase.html
More Resources/Practice: SRP.pdf, OCP.pdf, LSP.pdf, ISP.pdf, DIP.pdf, screencapture-q-utoronto-ca-courses-394773-quizzes-481354-history-2025-12-13-18_10_05.pdf, screencapture-q-utoronto-ca-courses-394773-quizzes-481343-history-2025-12-13-18_13_01.pdf
Sub-item: Your Project and SOLID: stakeholders, actors, user (Your%20Project%20and%20SOLID%20stakeholders,%20actors,%20user%202c8e7be659d9808787c6c66cac925f34.md)

# SOLID Principles

1. ***Single responsibility principle* (SRP):** a class should have only one reason to change
2. ***Open/closed principle* (OCP)**: a class should be open for extension but closed for modification
3. ***Liskov substitution principle* (LSP)**: subclasses should be substitutable for their base classes
4. ***Interface segregation principle* (ISP)**: programmers should not be forced to write or rely on interface methods they do not use
5. ***Dependency inversion principle* (DIP)**: high-level modules should not depend on low-level modules. Both should depend on abstractions.

## 1. SRP

[https://blog.cleancoder.com/uncle-bob/2014/05/08/SingleReponsibilityPrinciple.html](https://blog.cleancoder.com/uncle-bob/2014/05/08/SingleReponsibilityPrinciple.html)

“Gather together the things that *change* for the same reasons. Separate those things that change for different reasons."

I.e., 

Each class should have at most one source of change

Each class should have at most one stakeholder

- high cohesion; low coupling
- An ***actor*** (a **user** of the program or a **stakeholder** — or a group of such people — or even an automated process) causes the change
- Goal: design classes that are easier to understand, test, and modify by ensuring that each class responds to a single, well-defined reason for change
- ⇒ Work is divided up to specific people responsible for the reason of change, and no two people would try to change/update a single file at the same time

## 2. OCP

you should be able to add new functionality to a program without modifying the existing code

via functionality added by extending existing code — through inheritance, interfaces, or composition

extension = adding new subclasses or adding new features/classes/etc

## 3. LSP

Formally, if S is a subtype of T, then objects of type S may be substituted for objects of type T, without altering any of the desired properties of the program; I.e., you should be able to replace an instance of Person (parent class) with an instance of Student (subclass) without *breaking the program*

By *breaking the program*, it’s beyond just ensuring the program runs but also ensuring no core/expected functionalities/logic is disrupted/missing

In Java, T could be a class or an interface. S will either extend class T, or S will implement interface T.

- I.e., subtype S shouldn’t be more contrained — or have less functionality — than type T
- e.g., a Student subclass of Person superclass shouldn’t have max. age of 200 when Person has max. age of 100
- e.g., a subclass shouldn’t throw exceptions that the superclass doesn’t expect

## 4. ISP

Don’t make your interfaces too big (but shouldn’t be too small either — not covered by ISP though)

- Consider a case where your class depends on a `Service` interface that provides several methods: `m1`, `m2`, and `m3`. If your class only uses `m1`, then any change to `m2` or `m3` — even if unrelated to your needs — will still require your class to be recompiled and possibly retested.
- Consider if you have an interface `Animal` with methods `eat`, `sleep`, and `fly`, a class `Dog` that implements `Animal` would be forced to implement the `fly` method, which is irrelevant for dogs.

## 5. DIP

***module*** - a class or a set of closely-related classes

High level modules and low level modules should all depend on abstractions as much as possible; I.e., depend on a parent class as much as possible

**low level class** - class that knows the specific details of program

**high level class** - class entities that don’t know anything about the details of the program, and is just involved on storing information (e.g., doesn’t call methods from other classes)

![image.png](image%206.png)

Note:  `HighLevel` is tightly coupled to the implementation details of `LowLevel`, so any change in `LowLevel` could affect `HighLevel`!

![image.png](image%207.png)

Note: nothing points at `LowLevel` anymore → can freely replace `LowLevel` with a different implementation

Note: we need to take great care to define interfaces (`Interface`) that are stable and unlikely to require change in the future

Example: [http://www.oodesign.com/dependency-inversion-principle.html](http://www.oodesign.com/dependency-inversion-principle.html)

![image.png](image%208.png)