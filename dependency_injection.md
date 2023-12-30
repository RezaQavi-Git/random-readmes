# Description

Dependency injection is a technique whereby one object (or static method) supplies the dependencies of another object. A dependency is an object that can be used.

Transferring the task of creating the object to someone else and directly using the dependency is called dependency injection.

- Dependencies can be injected at runtime rather than at compile time
- States that a class should depend on abstraction and not upon concretions (in simple terms, hard-coded).

# Types of dependency injection:
1. constructor injection: the dependencies are provided through a class constructor.
2. setter injection: the client exposes a setter method that the injector uses to inject the dependency.
3. interface injection: the dependency provides an injector method that will inject the dependency into any client passed to it. Clients must implement an interface that exposes a setter method that accepts the dependency.


# Benefits of using DI

1. Helps in Unit testing.
2. Boiler plate code is reduced, as initializing of dependencies is done by the injector component.
3. Extending the application becomes easier.
4. Helps to enable loose coupling, which is important in application programming.

# Disadvantages of DI
1. It’s a bit complex to learn, and if overused can lead to management issues and other problems.
2. Many compile time errors are pushed to run-time.
3. Dependency injection frameworks are implemented with reflection or dynamic programming. This can hinder use of IDE automation, such as “find references”, “show call hierarchy” and safe refactoring.

References:
- [freecodecamp](https://www.freecodecamp.org/news/a-quick-intro-to-dependency-injection-what-it-is-and-when-to-use-it-7578c84fa88f/)