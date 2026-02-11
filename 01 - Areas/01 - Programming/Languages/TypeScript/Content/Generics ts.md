#typescript 

---

**Generics** are used to define how a function/class/interface/type will be acting with the values and their types.

```ts
funciton func<T>(arg1: T): T {...}
//            ^ definition of type "variable" that will be used
//                     ^ arg1 of the func should be of type T
//                         ^ what type is gonna be returned 
```

## Generic Constraints

These are used to restrict the types of Generics.

**K** *must be* the *key of* **T**:  
```ts
function func<T, K extends keof T>(...
```

**T** *must be* a *number*:
```ts
function func<T extends number>(...
```

**T** *must have* an internal *id property*:
```ts
function func<T extends {id: number}>(...
```

**T** is an array:
```ts
function func<T>(arg: T[])...
```


could also be something like that:
```ts
type PaginatedApiResponse<T> = ApiResponse<PaginatedResponse<T>>;
```
