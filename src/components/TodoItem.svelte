<script>
    import {v4 as uuid} from 'uuid'
    import {createEventDispatcher} from "svelte";
    export let title
    export let done

    const dispatch = createEventDispatcher()

    function handleDoneChange(event) {
        dispatch('doneChange', event.target.checked)
    }
    function handleRemoveClick() {
        dispatch('remove')
    }
</script>

<div class="main-container">
    <input
            checked={done}
            type="checkbox"
            on:input={handleDoneChange}
    />
    <p class="title">{title}</p>
    <p class="remove-button"
       on:click={() => console.log('inline handler')}
       on:click={handleRemoveClick}
    >Remove</p>
</div>

<style>
    .main-container {
        display: flex;
        height: 50px;
        border-radius: 5px;
        align-items: center;
        background-color: darkseagreen;
        padding: 0 15px;
    }
    input {
        margin: 0;
        margin-right: 20px;
    }
    p {
        margin: 0;
    }
    .title {
        flex: 1;
    }
    .remove-button {
        color: brown;
        font-weight: bold;
        cursor: pointer;
    }
</style>