# Parts of a Program

Progress: New
: No
Parent item: RAT (RAT%20281e7be659d98064b3b1fac7f660de4d.md)
Practice: https://q.utoronto.ca/courses/394773/pages/m1-parts-of-a-program (+ https://github.com/CSC207-2025F-UofT/Trader)
More Resources/Practice: RestaurantReviewSpecification_(1).pdf

REVIEW:

ClassA is **dependant** on ClassB if a change to the code in ClassB could result in a change to the code in ClassA. In other words, ClassA calls methods or a constructor in ClassB.

We expect that an entity object should not depend on other objects. (sometimes entities depend on each other)

We can eliminate dependencies by introducing an interface.

We assume that interfaces will not change once everyone agrees on them.

```java
// Activity 1: Consider the code from the previous question. Which of the following statements is correct?

A. Main is dependent on Trader // <-

B. Trader is dependent on Main

C. Trader and Main are both dependent on each other

D. Neither class is dependent on the other.
```

```java
// Activity 2: Consider the code from the previous question. Which of the following statement is correct?

A. Hatchimal is dependent on Trader

B. Trader is dependent on Hatchimal

C. Trader and Hatchimal are both dependent on each other

D. Neither class is dependent on the other. // <-
```

Activity 4: Consider the following specification for a software system that facilitates restaurant reviews:

> Each restaurant corresponds to a certain price range, neighbourhood, and cuisines it serves. Restaurants that serve alcohol must have a license, which they need to renew every year. The system should also report how long, on average, customers wait for take out in restaurants that offer take-out service.
When reviewers leave a review for a restaurant, they must specify a recommendation (Thumbs Up or Thumbs Down) and can also leave a comment. An owner of a restaurant can respond to a review with a comment. All users of the system log in with their username. Users can choose to be contacted by email, text message, or not contacted at all when a review or comment they wrote has been approved by a moderator and posted.
A user can browse restaurant reviews randomly, search for one directly by restaurant name, group reviews according to location, or group reviews according to the style of food they serve.
> 
- How many nouns would you turn into classes in your program?
    
    5-6
    
    User
    
    Moderator
    
    RestaurantOwner
    
    Reviewer
    
    Restaurant
    
    RestaurantPropertyManager ← not an entity (shouldn’t depend on other objects) ⇒ no dependent on other classes
    
    License ← can discuss whether just needs to be a boolean of yes/no license or itself have properties
    
    Review
    
    [other potential classes are up to discussion]
    
    - restaurant
    - user
        - reviewers
        - owner
    - alcohol
    - take-out (interface)
    - review

[RestaurantReviewSpecification.pdf](RestaurantReviewSpecification.pdf)

Activity 5: User Stories

<aside>
💡

Template:

As a [role/perspective], I want to [specific action/feature/thing]

</aside>

- Consider the previous specification. How many user stories can be identified from what is currently included in the specification or implied by the features listed (such as a restaurant owner changing the properties of their listing when they first get a license to serve alcohol)?
    - As a user, I want to search for a restaurant that is licensed and ~~compare reviews~~ {be specific!} look through the top ranking results, listed by number of “thumbs up”.
    - As a user, I want to log into the system with my username and password to leave a review.
    - As a user, I want to choose to be contacted by email
    - …many more
    
    ⇒ depends on design of program, can have very specific user stories ⇒ D. More than 10
    

*- review pls October 17, 2025*