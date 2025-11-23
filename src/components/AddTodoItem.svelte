<script>
    import {afterUpdate, beforeUpdate, onDestroy, onMount, tick} from "svelte"
    import {onInterval} from "../utils/onInterval.js";
    import {getTodos} from "../utils/getTodos.js";
    import {format} from "../utils/format.js";
    import TodoItem from "./TodoItem.svelte";
    import {v4 as uuid} from 'uuid'

    export let title = "Enter what do you want to do:";
    export let buttonTitle = "Add todo";

    console.log($$props)
    console.log($$restProps)

    let items = []
    let counter = 0
    let counter2 = 0
    let interval

    onMount(() => {
        console.log('onMount')
        getTodos().then(value => {
            items = value;
        })

        // const get = async () => {
        //     items = await getTodos()
        // }
        // get()

        interval = setInterval(() => {
           counter++
        }, 1000)
        // the same as onDestroy
        return () => {
           clearInterval(interval)
        }
    })

    onDestroy(() => {
        clearInterval(interval)
    } )

    // the same as onMount, onDestroy
    onInterval(() => {
        counter2++
    }, 1000)

    beforeUpdate(() => {
        console.log('beforeUpdate')
    })

    afterUpdate(() => {
        console.log('afterUpdate')
    })

    function handleAddClick() {
        items = [...items, {
            id: uuid(),
            text: "Item text",
        }]
    }

    let text = ''
    async function handleTextChange(event) {
        const { selectionStart, selectionEnd, value } = this
        text = format(event.target.value)

        await tick()
        this.selectionStart = selectionStart
        this.selectionEnd = selectionEnd
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

{counter}
<br>
{counter2}
<div class="main-container">
    <label for="todo-text">{title}</label>
    <input class="todo-input" id="todo-text"
        value={text}
        on:input={handleTextChange}
    />
    <button on:click={handleAddClick}>{buttonTitle}</button>
</div>

{#if items.length === 0}
    No items yet
{:else if items.length === 4}
    You have 4 items to do
{:else }
    {#each items as {id, text}, index (id)}
        <TodoItem title={`${index + 1}: ${text}`} />
    {:else }
        No items yet
    {/each}

    {JSON.stringify(items, null, 2)}
{/if}

<br>
<!--{@debug items}-->
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