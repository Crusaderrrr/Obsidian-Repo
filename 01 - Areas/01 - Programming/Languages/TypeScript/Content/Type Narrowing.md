Means that if we have united two or more types and in any place of the code we want to use them separately:

1. **Classic if-else**:
```ts
function(arg: number | string | null) {
	if (typeof arg === "number") {
		return
	} else if (typeof arg === "string") {
		return
	}
	
	return arg;
}
```
here ts understands which type we are checking.

2. **Using docs approach**:
```ts
function(arg: number | string | null) {
	if (arg === null) {
		return
	} 
	
	return arg;
}
```
Just compare using 3 equality signs.


## Narrowing for Interfaces

```ts
interface User {
	username: string;
	age: number;
}

interface Person {
	lastname: string;
	firstname: string;
	age: number;
}

function(arg: User | Person) {
	if ("username" in arg) {
		arg
	}
	
	if ("firstname" in arg) {
		arg
	}
}
```


## Narrowing in Classes
