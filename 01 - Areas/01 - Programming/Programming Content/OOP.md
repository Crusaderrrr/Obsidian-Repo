---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - patterns
note type: Informational Note
---
*Object-Oriented Programming* (OOP) is a programming paradigm that organizes software design around data, or objects, rather than functions and logic. An object is a data structure that contains both data (attributes or properties) and methods (functions) that operate on the data. OOP is commonly used in software design because it promotes modularity, code reuse, and scalability.

There are 4 **core principles**: 
1. **Encapsulation**
	It means that the internal object’s state is hidden and can be accessed only via *getters* and *setters*, also it means creating strict methods that are used to manipulate the object. OOP based languages provide mechanisms like *private*, *protected*, *public* to enforce encapsulation.
	
	**Analogy**: Like a car where the internal mechanics (engine, transmission) are hidden under the hood and users interact only through controls (steering wheel, pedals), encapsulation hides the complex inner workings of a class and exposes a simple interface.
2. **Inheritance** 
	Inheritance allows a new class (child or subclass) to *inherit* (override) the properties and methods of an existing class (parent or superclass). This mechanism supports code reuse and establishes a hierarchical relationship between classes.
3. **Polymorphism** 
	Allows the same action or method to work differently for different objects. In other words, different classes can define their own unique versions of the same method, and you can use these objects interchangeably through a common interface.
4. **Abstraction**
	Abstraction involves hiding the complex implementation details of an object and exposing only the necessary features. This principle helps reduce complexity and allows programmers to interact with objects at a higher level, focusing on what the object does rather than how it does it.

Moreover there are two important concepts: 
- **Composition** 
	This is when some object consists of other objects, like a car for example it has 4 wheel objects 4 seat objects, etc. All of these objects are intitialized *inside the constructor*. Builds a *relationship “has-a”*. 
- **Aggregation** 
	This is a smelling tree, it stays outside the car object but can be introduced there by someone. The freshener is initialized *outside the constructor* and doesn’t relate to this class. 
- **If we delete** `Car` class all the wheels, engine, etc will be deleted, though the freshener won’t. 

## Relative Info
- [[Abstract classes]]