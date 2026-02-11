#typescript #programming 

*literally types*
1. `any`
	**Disables all type checking** and represents any type.
2. `never`
	**Values that never occur** and the empty set of values
3. `unknown`
	A type-safe alternative to `any`, requires **type check before use**
4. `void`
	The **absence of any type**, mostly used for functions

*Logic types*
1. `|` union (one of several)
2. `&` intersection (AND logic)

#### Examples

- `any`
```ts
let data: any = 42;
data = "hello";        // OK - no type checking
data = [1, 2, 3];      // OK - accepts anything
data.someMethod();     // OK - TypeScript won't complain
```

- `never`
```ts
function throwError(message: string): never {
  throw new Error(message);  // Never returns normally
}

type Shape = "circle" | "square";
function getArea(shape: Shape): number {
  switch (shape) {
    case "circle": return 3.14;
    case "square": return 16;
    default:
      const _exhaustive: never = shape;  // Ensures all cases handled
      return _exhaustive;
  }
}
```

- `unknown`
```ts
let value: unknown = "hello";

// Error: can't use directly
console.log(value.toUpperCase());

// OK: must check type first
if (typeof value === "string") {
  console.log(value.toUpperCase());  // Now TypeScript knows it's a string
}
```

- `void`
```ts
function logMessage(msg: string): void {
  console.log(msg);
  // No return statement - function returns undefined
}

let result: void = undefined;  // Only undefined can be assigned
```

- Union
```ts
let value: string | number;
value = "hello";  // Valid
value = 42;       // Valid

type Status = "success" | "error" | "pending";

function format(input: string | number): string {
  if (typeof input === "string") {
    return input.toUpperCase();
  }
  return input.toFixed(2);
}
```

- Intersection
```ts
type Name = { name: string };
type Age = { age: number };
type Person = Name & Age;

const person: Person = {
  name: "Alex",
  age: 30  // Must have BOTH properties
};

type Draggable = { drag: () => void };
type Resizable = { resize: () => void };
type UIWidget = Draggable & Resizable;

const widget: UIWidget = {
  drag: () => console.log("dragging"),
  resize: () => console.log("resizing")
};
```