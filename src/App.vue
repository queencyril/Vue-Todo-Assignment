<template>
  <div id="app">
    <div>
      <h1>MY DAILY TODO.....</h1>
    </div>

    <div>
      <input type="text" v-model="todo" placeholder="add todo..." />
      <div>
        <button @click="addTodo" id="display">Add</button>
        <button @click="clearAllTodo" id="display">Clear List</button>
      </div>
    </div>

    <div v-for="(todo, index) in todos" v-bind:key="index">
      <ul>
        <li>
          <div class="my-todo">{{ todo.text }}</div>
        </li>
      </ul>
      <button id="del" @click="removeTodo(index)">Delete</button>
      <button @click="editTodo(index)">Edit</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      todo: "",
      editedTodoText: null,
      todos: [],
    };
  },

  methods: {
    addTodo() {
      if (this.todo.length === 0) return;
      if (this.editedTodoText !== null) {
        this.todos[this.editedTodoText].text = this.todo;
        this.editedTodoText = null;
        this.todo = "";
      } else {
        this.todos.push({
          text: this.todo,
        });
        this.todo = "";
      }
    },

    removeTodo(todoId) {
      this.todos = this.todos.filter((todo) => todo.id !== todoId);
    },

    editTodo(index) {
      console.log(index);
      (this.todo = this.todos[index].text), (this.editedTodoText = index);
    },

    clearAllTodo() {
      this.todos = [];
    },
  },
};
</script>

<style scoped>
#app {
  min-width: 300px;
  min-height: 300px;
  display: flex;
  place-content: center;
  justify-content: center;
  align-items: center;
  border: 2px dotted pink;
  display: block;
}

h1 {
  font-size: 35px;
  font-family: monospace;
  color: rgba(196, 5, 170, 0.349);
  text-align: center;
}

input {
  padding: 10px 50px;
  width: 100%;
  border-radius: 10px;
  font-size: 12px;
  border-color: pink;
  border-left: 0;
  border-right: 0;
  text-align: center;
  margin-top: 20px;
}

button {
  margin: 5px;
  border: 2px dashed rgba(128, 0, 117, 0.24);
  font-size: 20px;
  font-weight: 200;
  color: rgba(75, 48, 52, 0.89);
  border-radius: 20px;
  border: 1px solid transparent;
  padding: 3px 20px;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  cursor: pointer;
  transition: border-color 1s;
  background-color: rgba(211, 191, 208, 0.534);
}

button:hover {
  border-color: #ff64dd;
}

#display {
  padding: 8px 60px;
  border-radius: 0;
  margin-bottom: 20px;
}

ul li {
  font-size: 20px;
  color: rgba(75, 48, 52, 0.89);
}

#del {
  background-color: pink;
  color: white;
}

@media (max-width: 414px) {
  .container {
    margin-top: 80px;
    max-width: 300px;
  }
}
</style>
