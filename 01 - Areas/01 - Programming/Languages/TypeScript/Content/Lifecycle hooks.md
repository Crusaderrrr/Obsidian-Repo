Basically, there are some hooks such as `useEffect` from ReactJS:

- `onMount` 
```ts
<script>
	import { onMount } from 'svelte';

	onMount(() => {
		const interval = setInterval(() => {
			console.log('beep');
		}, 1000);

		return () => clearInterval(interval);
	});
</script>
```
If the *callback is returned* it acts as a cleaner function that is *executed on component unmount*.

- `onDestroy`
Schedules a callback to run **immediately before the component is unmounted**.
```ts
<script>
	import { onDestroy } from 'svelte';

	onDestroy(() => {
		console.log('the component is being destroyed');
	});
</script>
```

- `tick`
Returns a promise that resolves once pending *state changes have been applied to the DOM*. This is useful when you need to wait for the DOM to update before performing an action.