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
  </style>
  
  <main>
	<input bind:value={taskInput} placeholder="Enter a task" />
	<button on:click={addTask}>Add Task</button>
  
	<!-- This is where the list, appearing as a large rectangle, will be -->
	<ul>
	  {#each tasks as task (task.id)}
		<li>
		  <input type="checkbox" bind:checked={task.done} />
		  <span class={task.done ? 'done' : ''}>{task.text}</span>
		  <button on:click={() => deleteTask(task.id)}>Delete</button>
		</li>
	  {/each}
	</ul>
  
	<p>{unfinishedCount} unfinished task(s)</p>
  </main>
  