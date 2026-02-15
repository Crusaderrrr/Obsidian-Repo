This is a **global accessible object** that *hold a values* and allow components to subscribe to changes.

Simples example:
```ts
<script>
	import { writable } from 'svelte/store';

	const count = writable(0);
	console.log($count); // logs 0

	count.set(1);
	console.log($count); // logs 1

	$count = 2;
	console.log($count); // logs 2
</script>
```

**Types of Stores**:
1. `writable` - a function that creates a store that can be *set or updated* from outside.
2. `readable` - a *read-only* store that can be set or updated only from where it is defined.
3. `derived` - a store which value is computed based on other stores on change.
4. custom store