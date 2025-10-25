#frontend #svelte

Components are basic building blocks of Svelte. To create a component we need to create `.svelte file`. Here we write scripts and html, css code

```svelte
<script lang="ts">
	let var = 'Hello';
</script>

<h1> {var + ' world!'} </h1>
```

In `{}` we can use any javascript we want.
Inside of the components we can write typical html style:

```svelte
<p>This is a paragraph.</p>

<style>
	p {
		color: pink;
		font-family: 'Comic Sans MS', cursive;
		font-size: 5em;
	}
</style>
```

---
[[Svelte]]