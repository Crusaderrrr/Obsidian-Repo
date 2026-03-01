These are very useful and many libraries are based on these.

**Quick example**:
```ts
type isArray<T> = T extends any[] ? true : false;
```
- checks if the type is an array 

Could be used like that:
```ts
const first:isArray<string> = false; //no error string != array
const second:isArray<string[]> = true; //no error string[] == array

const third:isArray<string> = true; //eslint error, string != array
```