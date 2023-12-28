# Design Pattern

## Definition

- Design patterns are design level solutions for recurring problems that we software engineers come across often.
- Design Patterns give you a shared vocabulary with other developers

## Types of Design Patterns

1. Creational: These patterns are designed for class instantiation. They can be either class-creation patterns or object-creational patterns.

2. Behavioral: These patterns are designed depending on how one class communicates with others.

3. Structural: These patterns are designed with regard to a class's structure and composition.

## Design Pattern List

### The Strategy Pattern

The Strategy Pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable.
Strategy lets the algorithm vary independently from clients that use it.

### Observer Pattern

Publishers + Subscribers = Observer Pattern

The Observer Pattern defines a one-to-many dependency between objects so that when one object changes state, all of its dependents are notified and updated automatically.

### Examples

- Type 1: Creational - The Singleton Design Pattern

  The Singleton Design Pattern is a Creational pattern, whose objective is to create only one instance of a class and to provide only one global access point to that object.

- Type 2: Structural - The Decorator Design Pattern

  The decorator design pattern falls into the structural category, that deals with the actual structure of a class, whether is by inheritance, composition or both. The goal of this design is to modify an objects’ functionality at runtime.

- Type 3: Behavioral - The Command Design Pattern

  A behavioral design pattern focuses on how classes and objects communicate with each other. The main focus of the command pattern is to inculcate a higher degree of loose coupling between involved parties

### References

- [Freecodecamp](https://www.freecodecamp.org/news/the-basic-design-patterns-all-developers-need-to-know/)
- [Sourcemaking](https://sourcemaking.com/design_patterns)
- [Head First Design Patterns](./books/head_first_design_patterns.md)
