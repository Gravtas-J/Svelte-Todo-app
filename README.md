## My Svelte To-Do App

Welcome to the documentation for my simple To-Do App built with Svelte!

### Overview:
I built this app to grasp the basics of Svelte, and I'm happy to walk you through the logic and structure of my code. It's a straightforward application that lets users add, mark as done, and delete tasks.

### How I Structured the Data:

1. **Tasks Array**: 
    - I used an array named `tasks` to store all the task items. Each task is an object with `id`, `text`, and `done` properties:
        - `id`: I used a timestamp as a unique identifier for every task.
        - `text`: It holds the description of the task.
        - `done`: A boolean flag to indicate if a task is completed or not.

2. **Task Input**: 
    - For capturing user inputs, I used a variable `taskInput`. This gets updated with whatever the user types into the input field.

### My Functions:

1. **addTask**: 
    - When the "Add Task" button is clicked, this function gets triggered. I check if the `taskInput` isn't just whitespace and then append a new task object to our `tasks` array. After adding, I clear out the `taskInput`.

2. **deleteTask**: 
    - For every task, I've provided a "Delete" button. When pressed, it calls this function with the task's unique `id`. I then filter out the task with the matching `id` from our `tasks` array.

3. **toggleDone**: 
    - Each task has a checkbox. I use this function to toggle the `done` status of a task. Whenever a checkbox is clicked, I map through the `tasks` array and flip the `done` flag of the task with the matching `id`.

### How I Displayed the Data:

- For rendering each task, I relied on Svelte's `{#each ...}` loop. Inside this loop:
    1. I rendered a checkbox that is bound to the task's `done` status.
    2. I showed the task's text. If a task is marked as done, I applied a `done` class to strike through the text.
    3. I included a "Delete" button to remove the task.

### Reactive Count:
- I wanted to show how many tasks were left unfinished. For this, I created a reactive statement `$: unfinishedCount` that recalculates the number of tasks not marked as `done` every time our `tasks` array gets updated.

### Styling:

- To visually differentiate between finished and unfinished tasks, I created a CSS class named `.done` that applies a line-through to the text.

