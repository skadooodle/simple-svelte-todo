<script>
    export let todo;
    function handleClick() {
        todo.done = !todo.done;
    }
</script>

<style>
    p {
        user-select: none;
        cursor: pointer;
        font-size: 2em;
        overflow-wrap: anywhere;
    }
</style>


{#if !todo.done}
<!-- svelte-ignore a11y-click-events-have-key-events -->
<p on:click={handleClick}>{todo.task}</p>
{/if}

{#if todo.done}
<!-- svelte-ignore a11y-click-events-have-key-events -->
<p on:click={handleClick}><s>{todo.task}</s> 👍</p>
{/if}