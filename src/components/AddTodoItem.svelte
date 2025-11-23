<script>
    export let title = "Enter what do you want to do:";
    export let buttonTitle = "Add todo";

    console.log($$props)
    console.log($$restProps)

    let items = []

    function handleAddClick() {
        items = [...items, 'item']
    }

    $: console.log("logs", items)

    $: if (items.length > 5) {
        console.log("logs", items)
    }

    $: {
        if (items.length > 5) {
        console.log("logs", items)
        }
    }
</script>

<div class="main-container">
    <label for="todo-text">{title}</label>
    <input class="todo-input" id="todo-text"/>
    <button on:click={handleAddClick}>{buttonTitle}</button>
</div>

<style>
    :global(label) {
        color: blueviolet;
    }
    .main-container {
        background-color: lightseagreen;
        border-radius: 5px;
        padding: 10px;
    }
    .todo-input {
        width: 100%;
    }
</style>