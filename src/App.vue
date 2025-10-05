<template>
  <div id="app">
    <h1>Gestor de Tareas</h1>

    <div class="input-container">
      <input v-model="newTask" type="text" placeholder="Escribe una tarea..." />
      <button @click="addTask">Agregar</button>
    </div>

    <div class="boards">
      <div class="board">
        <h2>To Do</h2>
        <div v-if="tasks.todo.length === 0" class="empty">Vacío</div>
        <div v-for="(task, index) in tasks.todo" :key="'todo-' + index" class="task">
          {{ task }}
          <div class="actions">
            <button @click="moveTask('todo', 'doing', index)">➡</button>
          </div>
        </div>
      </div>

      <div class="board">
        <h2>Doing</h2>
        <div v-if="tasks.doing.length === 0" class="empty">Vacío</div>
        <div v-for="(task, index) in tasks.doing" :key="'doing-' + index" class="task">
          {{ task }}
          <div class="actions">
            <button @click="moveTask('doing', 'todo', index)">⬅</button>
            <button @click="moveTask('doing', 'done', index)">➡</button>
          </div>
        </div>
      </div>

      <div class="board">
        <h2>Done</h2>
        <div v-if="tasks.done.length === 0" class="empty">Vacío</div>
        <div v-for="(task, index) in tasks.done" :key="'done-' + index" class="task">
          {{ task }}
          <div class="actions">
            <button @click="moveTask('done', 'doing', index)">⬅</button>
            <button class="delete" @click="deleteTask('done', index)">✖</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      newTask: "",
      tasks: {
        todo: [],
        doing: [],
        done: [],
      },
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== "") {
        this.tasks.todo.push(this.newTask);
        this.newTask = "";
      }
    },
    moveTask(from, to, index) {
      const task = this.tasks[from].splice(index, 1)[0];
      this.tasks[to].push(task);
    },
    deleteTask(section, index) {
      this.tasks[section].splice(index, 1);
    },
  },
};
</script>

<style>
body {
  background-color: #222;
  color: #f4f4f4;
  font-family: "Poppins", sans-serif;
  text-align: center;
  margin: 0;
  padding: 0;
}

#app {
  padding: 40px;
}

h1 {
  font-size: 2.5rem;
  margin-bottom: 20px;
}

.input-container {
  margin-bottom: 30px;
}

input {
  padding: 8px;
  width: 250px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #fff;
  color: #000; /* ✅ texto negro visible */
  font-size: 1rem;
}

input::placeholder {
  color: #888;
}

button {
  margin-left: 10px;
  padding: 8px 12px;
  background-color: #28a745;
  border: none;
  color: white;
  border-radius: 5px;
  cursor: pointer;
  font-weight: bold;
  transition: background 0.2s;
}

button:hover {
  background-color: #218838;
}

.boards {
  display: flex;
  justify-content: center;
  gap: 20px;
}

.board {
  background-color: #eee;
  color: #222;
  padding: 20px;
  border-radius: 10px;
  width: 200px;
  min-height: 250px;
  text-align: center;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.board h2 {
  color: #555;
  margin-bottom: 10px;
}

.task {
  background-color: #fff;
  color: #000;
  border-radius: 5px;
  padding: 8px;
  margin-bottom: 8px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.task .actions button {
  margin: 0 3px;
  padding: 4px 6px;
  font-size: 0.9rem;
}

.task .delete {
  background-color: #dc3545;
}

.task .delete:hover {
  background-color: #c82333;
}

.empty {
  color: #777;
  font-style: italic;
  margin-top: 40px;
}
</style>
