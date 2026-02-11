---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - clean_code
note type: Informational Note
---
**General Responsibility Assignment Software Patterns** ( or Principles ). This is a list of 9 rules of how to assign responsibilities to classes and objects in OOP.

## Principles:

1. **Information Expert**
	*What it means:*  
	Give a job to the class that has the most information needed to do it.
	*Example:*  
	If you want to calculate the total price of items in a shopping cart, let the `ShoppingCart` class do it, since it knows about all the items.
2. **Creator**
	*What it means:*  
	Let the class that has or uses another class create it.
	*Example:*  
	A `Library` class manages many `Book` objects. The `Library` should create new `Book` objects, not some random class.
3. **Controller**
	*What it means:*  
	Have a class that handles user input and system events, then tells other classes what to do.
	*Example:*  
	When a user clicks “Submit Order,” an `OrderController` class receives the event, checks the order, and processes it.
4. **Low Coupling**
	*What it means:*  
	Classes should depend on each other as little as possible. This makes your code easier to change.
	*Example:*  
	If `Order` needs to send an email, instead of calling `EmailService` directly, it could use an interface. That way, you can swap out the email system later without changing `Order`.
5. **High Cohesion**
	*What it means:*  
	Keep related things together in one class. Each class should have a clear job.
	*Example:*  
	A `User` class should only handle user-related data and actions, not things like payment processing.
6. **Polymorphism**
	*What it means:*  
	Use the same method name for different behaviors, depending on the object type.
	*Example:*  
	A `draw()` method in a `Shape` interface. `Circle` and `Square` both implement `draw()`, but each draws itself differently.
7. **Pure Fabrication**
	*What it means:*  
	Sometimes you create a class just to keep your code clean, even if it doesn’t represent a real-world thing.
	*Example:*  
	A `Logger` class that just handles logging messages, instead of putting logging code everywhere.
8. **Indirection**
	*What it means:*  
	Use a middleman to connect classes, making them less dependent on each other.
	*Example:*  
	Instead of `Order` talking directly to `PaymentGateway`, use a `PaymentProcessor` interface in between. This way, you can change the payment gateway without changing `Order`.
9. **Protected Variations**
	*What it means:*  
	Protect parts of your code from changes elsewhere by using interfaces or abstract classes.
	*Example:*  
	If you have different ways to save data (like to a file or a database), use a `DataStore` interface. Your main code uses `DataStore`, so you can add new storage types without breaking things.