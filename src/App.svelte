<script>
	import { fade, fly } from "svelte/transition";
	import Header from "./components/Header.svelte";

	let todo = "";
	let todos = ["Todo 1", "Todo 2", "Todo 3", "Todo 4"];
	let validInput = false;

	function addNewTodo() {
	  todos.push(todo);
	  todos = todos;
	  todo = "";
	  validInput = false;
	}

	function removeTodo(index) {
	  todos.splice(index, 1);
	  todos = todos;
	}

	function verifyInput() {
	  if (todo == "" || todo.length == 0) {
	    validInput = false;
	  } else {
	    validInput = true;
	  }
	}
</script>

<style>
	.center {
	  text-align: center;
	}
	.list {
	  list-style: none;
	  color: #2c3e50;
	  font-size: 25px;
	}
	.item {
	  padding-bottom: 10px;
	}
	.remove-todo-btn {
	  padding-left: 80px;
	  color: #e74c3c;
	  cursor: pointer;
	}
	.remove-todo-btn:hover {
	  color: #c0392b;
	}
	.add-todo-btn {
	  color: #2ecc71;
	  cursor: pointer;
	}
	.add-todo-btn:hover {
	  color: #27ae60;
	}
</style>

<Header/>

<div class="container center" on:input={verifyInput}>
<h1>TODO APP</h1>
<hr><br>
<div class="row justify-content-md-center">
<ul class="list-group list">
{#each todos as todo, i}
	 <li in:fly="{{ y: 50, duration: 1000 }}" out:fly="{{ x: -200, duration: 1000 }}" class="list-item item"> {todo} <i class=" float-right fas fa-minus-circle remove-todo-btn" on:click={() => removeTodo(i)}></i></li>
{/each}
</ul>
</div>
<br>
{#if !validInput}
<div class="alert alert-info" role="alert">
  Please enter a task!
</div>
{/if}
<br>
<div class="row justify-content-md-center">
<div class="form-group col-md-4">
  <input type="text" class="form-control" bind:value={todo}>
</div>
<div class="col-md-1">
{#if validInput}
<i class="fas fa-plus-circle fa-2x add-todo-btn" on:click={addNewTodo}></i>
{/if}
</div>
</div>
</div>



