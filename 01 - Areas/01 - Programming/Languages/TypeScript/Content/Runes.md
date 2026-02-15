These are Svelte **keywords** with `$` sign before and are used to control the svelte's compiler.

- `$state`
Rune that is used *to make* a variable, object or class fields *reactive*. It means that if the `$state` has changed the application will react to it. Some examples:
```ts
<script>
	let count = $state(0); //here
</script>

<button onclick={() => count++}>
	clicks: {count}
</button>

//.....................................................................//

let todos = $state([
	{
		done: false,
		text: 'add more todos'
	}
]);

```
There are some nuances with exporting the state to other modules and also there is more about state in docs.

---

 - `$derived`
Creates a computed value based on the dependency change. Code example:
```ts
let { width, height } = $props();
let area = $derived(width * height);
```
here the *area* is calculated automatically when one of the dependency values (width, height) changes.

---

- `$effect`
Primarily used for *logging*, *fetching data* or *DOM manipulations* based on the dependency change:
```ts
let count = $state(0);

// runs when state var changes
$effect(() => {
  console.log(`Count changed to: ${count}`);
});
```

---

- `$props` 
 Props is what is getting passed to the component as properties.
 
 *Outside the component*:
 ```ts
 <script lang="ts">
	import MyComponent from './MyComponent.svelte';
</script>

<MyComponent adjective="cool" />
 ```

*Inside that component*:
```ts
<script lang="ts">
	let props = $props();
</script>

<p>this component is {props.adjective}</p>
```

*Also could be* (with fallback value):
```ts
<script lang="ts">
	let { adjective = 'happy' } = $props(); //destructuring values 
</script>

<p>this component is {adjective}</p>
```

---

- `$bindable`
Allows you to create **two-way data binding** between parent and child components.

Parent:
```ts
<script>
let message = $state('Hello');
</script>

<Child bind:value={message} />
<p>Parent sees: {message}</p>
```

Child:
```ts
<script>
let { value = $bindable() } = $props();
</script>

<input bind:value />
```