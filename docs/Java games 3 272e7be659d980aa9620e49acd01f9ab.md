# Java games 3

Progress: New
: No
Parent item: RAT (RAT%20281e7be659d98064b3b1fac7f660de4d.md)
Practice: https://q.utoronto.ca/courses/394773/pages/m1-java-games-part-3
More Resources/Practice: JavaMemoryModelExamples.pdf

```java
//Consider an online shopping program with class CartItem and class Pen which extends CartItem. Here we initialize x:
Pen x = new Pen();

//A.
getCartItem(x);
Where getCartItem is defined as:

public CartItem getCartItem(CartItem ci) {
  return ci;
}

//B.
  List<CartItem> inventory = new ArrayList<>();
  inventory.add(x);
  
//C.
((CartItem) x).setName();

//D.
//All of the above are examples of casting x as an object of type CartItem.
```

- Which of the above code snippets does NOT cast x as an instance of `CartItem`?
    
    D.
    

*- review pls October 17, 2025*