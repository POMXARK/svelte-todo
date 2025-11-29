<script>
    import AddTodoItem from "./components/AddTodoItem.svelte";
    import TodoItem from "./components/TodoItem.svelte";
    import {v4 as uuid} from 'uuid'
    import {todoItems} from "./store/customStore.js";
    export let name;

    let items = []

    function handleAddClick(event) {
        todoItems.add(event.detail)
    }

    function handleDoneChange(id, done) {
        todoItems.setDone(id, done)
    }

    function handleRemove(id) {
        todoItems.remove(id)
    }

</script>

<AddTodoItem on:add={handleAddClick} />

{$todoItems.filter(item => item.done).length}/{$todoItems.length}

{#each $todoItems as {id, text, done}, index (id)}
    <div class="todo-item-container">
        <TodoItem
                title={`${index + 1}: ${text}`}
                {done}
                on:doneChange={event => handleDoneChange(id, event.detail)}
                on:remove={() => handleRemove(id)}
        />
    </div>
{:else }
    No items yet
{/each}

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