<template>
  <div class="content">
    <div class="heading">
      <h1>Todo List</h1>
    </div>
    <div>
      <md-field>
        <md-input
          v-model="currentTodo"
          @keydown.enter="addTodo()"
          placeholder="Add a todo"
        ></md-input
      ></md-field>
      <ul class="todos" style="list-style:none">
        <li
          v-for="todo in todos"
          :key="todo.id"
          :class="{ isCompleted: todo.completed }"
        >
          <md-card class="md-primary" md-theme="purple-card" md-with-hover>
            <span
              @dblclick="editTodo(todo)"
              class="todo"
              :class="{ isCompleted: todo.completed }"
              :style="{ display: todo.edited }"
              >{{ todo.label }}</span
            >
            <input
              v-model="todo.label"
              @keydown.enter="editTodo(todo)"
              :class="{ isCompleted: todo.completed }"
              :style="{ display: todo.editing }"
              class="editTask"
            />
            <input
              type="checkbox"
              v-model="todo.completed"
              value="completed"
            /><span class="completedlabel">Completed</span>
            <button @click="removeTodo(todo)">Delete</button>
          </md-card>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: "",
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.currentTodo,
        completed: false,
        edited: "inline-block",
        editing: "none",
      });
      this.currentTodo = "";
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      todo.edited === "inline-block"
        ? (todo.edited = "none")
        : (todo.edited = "inline-block");
      todo.editing === "inline-block"
        ? (todo.editing = "none")
        : (todo.editing = "inline-block");
    },
  },
};
</script>

<style lang="scss" scoped>
@import "~vue-material/dist/theme/engine"; // Import the theme engine

@include md-register-theme(
  "default",
  (
    primary: md-get-palette-color(blue, A200),
    // The primary color of your application
      accent: md-get-palette-color(red, A200),
    // The accent or secondary color
      theme: light,
  )
);

@import "~vue-material/dist/theme/all"; // Apply the theme

@include md-register-theme(
  "purple-card",
  (
    primary: md-get-palette-color(purple, 500),
  )
);

@import "~vue-material/dist/base/theme";

@import "~vue-material/dist/components/MdCard/theme";

.md-card {
  width: 110%;
  margin-left: -43px;
  margin-bottom: 20px;
  height: 100px;
  font-family: "Domine";
}

.content {
  width: 500px;
  margin: 0 auto;
  display: block;
}

.todo {
  width: 200px;
  margin-left: 30px;
  margin-top: 30px;
  padding: 10px;
}

.isCompleted {
  text-decoration: line-through;
  color: #000;
}

.completedlabel {
  color: #000;
  margin: 5px;
}

.heading {
  width: 50%;
  margin-left: 200px;
}

button {
  background-color: black;
  color: red;
  margin: 20px;
}

.editTask {
  width: 200px;
  margin-left: 30px;
  margin-top: 30px;
  padding: 10px;
}
</style>
