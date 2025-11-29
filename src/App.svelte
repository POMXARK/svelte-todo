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
            done: false
        }]
    }

</script>

<AddTodoItem on:add={handleAddClick} />

{items.filter(item => item.done).length}/{items.length}

{#each items as {id, text, done}, index (id)}
    <div class="todo-item-container">
        <TodoItem
                title={`${index + 1}: ${text}`}
                bind:done={done}
        />
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