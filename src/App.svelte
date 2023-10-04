<script>
	let tasks = [];
	let taskInput = "";
  
	function addTask() {
	  if (taskInput.trim() !== "") {
		tasks = [...tasks, { id: Date.now(), text: taskInput, done: false }];
		taskInput = "";
	  }
	}
  
	function deleteTask(id) {
	  tasks = tasks.filter(task => task.id !== id);
	}
  
	$: unfinishedCount = tasks.filter(task => !task.done).length;
  </script>
  
  <style>
	.done {
	  text-decoration: line-through;
	}
  
	ul {
	  width: 300px; /* Or any desired width */
	  height: 400px; /* Or any desired height */
	  border: 2px solid #333; /* Border for the rectangle */
	  padding: 20px; 
	  background-color: #f4f4f4; /* Light gray background */
	  overflow-y: auto; /* Adds scrollbar if the tasks exceed the height */
	}
  
	li {
	  margin-bottom: 10px; /* Adds some space between tasks */
	}
	body, html {
    margin: 0;
    padding: 0;
    height: 100%; /* Ensure full viewport height */
    font-family: Arial, sans-serif; /* Optional: for better font styling */
	}

	main {
    display: flex;
    flex-direction: column;
    align-items: center; /* Center horizontally */
    justify-content: center; /* Center vertically */
    height: 100%; /* Use the full viewport height */
	}
  </style>
  
<main>
  <input bind:value={taskInput} placeholder="Enter a task" />
  <button on:click={addTask}>Add Task</button>
  <ul>
    {#each tasks as task (task.id)}
      <li>
        <input type="checkbox" bind:checked={task.done} />
        <span class={task.done ? 'done' : ''}>{task.text}</span>
        <button on:click={() => deleteTask(task.id)}>🗑️</button>
      </li>
    {/each}
  </ul>
  <p>{unfinishedCount} unfinished task(s)</p>
</main>
  