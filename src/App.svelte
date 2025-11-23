<script>
	import AddTodoItem from "./components/AddTodoItem.svelte";

    export let name;

    const props = {
        title: "What to do?",
        buttonTitle: "Go!",
        someProp: "some prop value",
    }

    let title = "What to do "
</script>

<main>
	<h1>Hello {name}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
</main>
<label for="">Some text</label>
<AddTodoItem title={("What to do " + "?").toLowerCase()}/>
<br>
<AddTodoItem {title} />
<br>
<AddTodoItem {...props} />


<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>