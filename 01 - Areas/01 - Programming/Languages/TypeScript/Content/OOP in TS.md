#typescript #oop 

**Consists of**:
- Classes
- Interfaces

### Classes
**When to use**:
- When we need to define behavior (methods, default values)
- Need a runtime type checking

- Can **extend** a single class at a time:
```ts
// ❌ This doesn't work
class Child extends Parent1, Parent2 {} // Syntax error
```
- but can extend multiple classes in an *inheritance structure*:
```ts
// ✅ This works - inheritance chain
class Animal {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
}

class Mammal extends Animal {
  warmBlooded = true;
}

class Dog extends Mammal {
  bark() {
    console.log("Woof!");
  }
}

const myDog = new Dog("Buddy");
// myDog has access to: name (from Animal), warmBlooded (from Mammal), bark (from Dog)
```

### Interfaces
**When to use**:
- To define a basic structure
- Creating *DTOs*, *API responses*, or data models
- When we want type checking to ​disappear after complying
- What we can possible need in multiple classes

- **many interfaces** can be implemented by a single class:
```ts
interface CanSwim {
  swim(): void;
}

interface CanFly {
  fly(): void;
}

interface HasName {
  name: string;
}

// ✅ Class implements three interfaces
class Duck implements CanSwim, CanFly, HasName {
  name: string;
}

const myDuck = new Duck("Donald");
myDuck.swim();
myDuck.fly();
```

# Main diff with Java

We can instantiate **Objects from interfaces in TypeScript**:
```ts
interface User {
	id: number;
	name: string;
}

//Object instance:
const user: User = {
	id: 1;
	name: "user";
}
```

*But*, in [[Java]] we can't do this.