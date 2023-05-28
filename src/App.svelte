<script>
  import { v4 as uuidv4 } from "uuid"
  import Todo from './lib/Todo.svelte'
  let todos = JSON.parse(localStorage.getItem('todos')) || [];
  let todoInput

  $: todos, localStorage.setItem('todos', JSON.stringify(todos));

  function clearTodos() {
    todos = todos.filter(todo => !todo.done)
  }
  function addTodo() {
    if (todoInput.replaceAll(" ", "") != "") {
    todos = [...todos, {id: uuidv4(), task: String(todoInput), done: false}]
    todoInput = ""
    }
    else {todoInput = ""}
  }

</script>

<style>
  input {
    width: 10vw
  }
  input, button {
    display: inline;
    margin-left: 0.5em;
  }
  div {
    display: inline-block;
    text-align: center
  }
  form {
    display: inline-block;
  }
</style>

<main>
  <div>
    <form on:submit|preventDefault={addTodo}>
      <input type="text" bind:value={todoInput}/>
      <button>📨</button>
    </form>

    <button on:click={clearTodos}>Clear ✅</button>
  </div>
  <p>{todos.filter(todo => todo.done).length} of {todos.length}</p>
  {#each todos as todo (todo.id)}
    <Todo bind:todo={todo}/>
  {/each}
</main>