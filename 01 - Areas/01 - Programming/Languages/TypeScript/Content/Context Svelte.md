This feature is used to **pass values from parent to child without passing them as props** (prop-drilling).

*Simple example*:
```ts
// Parent
<script lang="ts">
	import { setContext } from 'svelte';

	setContext('my-context', 'hello from Parent.svelte');
</script>

// Child
<script lang="ts">
	import { getContext } from 'svelte';

	const message = getContext('my-context');
</script>

<h1>{message}, inside Child.svelte</h1> 
```

Also `$state` can be used in context.