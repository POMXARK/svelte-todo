<script>
    import AddTodoItem from "./components/AddTodoItem.svelte";
    import {createEventDispatcher, onMount} from "svelte";
    import TodoItem from "./components/TodoItem.svelte";
    import {getTodos} from "./utils/getTodos.js";
    import {v4 as uuid} from 'uuid'
    export let name;

    // const props = {
    //     title: "What to do?",
    //     buttonTitle: "Go!",
    //     someProp: "some prop value",
    // }

    let title = "What to do "

    let items = []

    onMount(() => {
        console.log('onMount')
        getTodos().then(value => {
            items = value;
        })
    })

    function handleAddClick(event) {
        items = [...items, {
            id: uuid(),
            text: event.detail,
        }]
    }

</script>

<main>
    <h1>Hello {name}!</h1>
    <p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
</main>
<label for="">Some text</label>
<AddTodoItem on:add={handleAddClick} />

{#each items as {id, text}, index (id)}
    <div class="todo-item-container">
        <TodoItem title={`${index + 1}: ${text}`} />
    </div>
{:else }
    No items yet
{/each}

<!--<AddTodoItem title={("What to do " + "?").toLowerCase()}/>-->
<!--<br>-->
<!--<AddTodoItem {title} />-->
<!--<br>-->
<!--<AddTodoItem {...props} />-->


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