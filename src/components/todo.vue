<template>
  <div class="main">
    <h2>To-Do List</h2>
    <h4>What needs to be done?</h4>
    <template v-if="isEditing">
      <input type="text" v-model="newTodo" /><br />
      <button @click="updateTodo">Update Todo</button>
    </template>
    <template v-else>
      <input type="text" v-model="newTodo" /><br />
      <button @click="addTodo">Add</button>
    </template>
    <list-item
      v-for="todo in todos"
      :key="todo.id"
      :done="todo.isDone"
      @isChecked="(val) => (todo.isDone = val)"
      @delete="() => removeTodo(todo)"
      @edit="() => editTodo(todo)"
    >
      <span>{{ todo.text }}</span>
    </list-item>
  </div>
</template>

<script>
import ListItem from "./ListItem.vue";

let id = 0;
export default {
  name: "ToDo",
  data() {
    return {
      todos: [
        { id: id++, text: "Item1", isDone: false },
        { id: id++, text: "Item2", isDone: false },
        { id: id++, text: "Item3", isDone: false },
      ],
      newTodo: "",
      isEditing: false,
      current: null,
    };
  },
  components: {
    ListItem,
  },
  methods: {
    addTodo() {
      if (this.newTodo) {
        this.todos.push({ id: id++, text: this.newTodo, isDone: false });
        this.newTodo = "";
      }
    },
    removeTodo(todo) {
      console.log(todo.text);
      this.todos = this.todos.filter((t) => t !== todo);
    },
    editTodo(todo) {
      this.isEditing = true;
      console.log(todo);
      this.current = todo;
      this.newTodo = todo.text;
    },
    updateTodo() {
      this.current.text = this.newTodo;
      this.current = null;
      this.newTodo = "";
      this.isEditing = false;
    },
  },
};
</script>

<style scoped>
input {
  width: 100%;
  margin-bottom: 5px;
}
button {
  margin: 5px 0px;
  width: 100%;  
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-weight: bold;
}
.main {
  margin: 10px;
  padding: 10px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
span {
  margin-left: 4px;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  color: rgb(56, 48, 48);
}
</style>