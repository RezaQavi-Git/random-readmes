# SOLID

The SOLID Principles are five principles of Object-Oriented class design.

To create understandable, readable, and testable code that many developers can collaboratively work on.

# Detail

### The Single Responsibility Principle
The Single Responsibility Principle states that a class should do one thing and therefore it should have only a single reason to change.


### The Open-Closed Principle
The Open-Closed Principle requires that classes should be open for extension and closed to modification.
- Modification means changing the code of an existing class, and extension means adding new functionality.


### The Liskov Substitution Principle
The Liskov Substitution Principle states that subclasses should be substitutable for their base classes.
- This means that, given that class B is a subclass of class A, we should be able to pass an object of class B to any method that expects an object of class A and the method should not give any weird output in that case.


### The Interface Segregation Principle
Segregation means keeping things separated, and the Interface Segregation Principle is about separating the interfaces.
- The principle states that many client-specific interfaces are better than one general-purpose interface. Clients should not be forced to implement a function they do no need.
- Large interfaces should divided into small ones.


### The Dependency Inversion Principle
The Dependency Inversion principle states that our classes should depend upon interfaces or abstract classes instead of concrete classes and functions.

_If the OCP states the goal of OO architecture, the DIP states the primary mechanism_

References:
- [freecodecamp](https://www.freecodecamp.org/news/solid-principles-explained-in-plain-english/)
- [digitalocean](https://www.digitalocean.com/community/conceptual-articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design)