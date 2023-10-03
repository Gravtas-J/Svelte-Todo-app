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
  
	function toggleDone(id) {
	  tasks = tasks.map(task => 
		task.id === id ? {...task, done: !task.done } : task
	  );
	}
  
	$: unfinishedCount = tasks.filter(task => !task.done).length;
  </script>
  
  <style>
	.done {
	  text-decoration: line-through;
	}
  </style>
  
  <main>
	<input bind:value={taskInput} placeholder="Enter a task" />
	<button on:click={addTask}>Add Task</button>
  
	<ul>
	  {#each tasks as task (task.id)}
		<li>
		  <input type="checkbox" bind:checked={task.done} on:change={() => toggleDone(task.id)} />
		  <span class={task.done ? 'done' : ''}>{task.text}</span>
		  <button on:click={() => deleteTask(task.id)}>Delete</button>
		</li>
	  {/each}
	</ul>
  
	<p>{unfinishedCount} unfinished task(s)</p>
  </main>
  