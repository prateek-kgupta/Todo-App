<template>
  <div class="listItem" :class="`${done ? 'complete' : 'uncomplete'}`">
    <div class="inputField">
      <input type="checkbox" v-model="checkboxValue" />
      <slot></slot>
    </div>
    <div class="buttonField">
      <button @click="editTodo">Edit</button>
      <button @click="removeTodo">Delete</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ListItem",
  data() {
    return {
      checkboxValue: false,
    };
  },
  emits: ["delete", "edit", "isChecked"],
  props: ["done"],
  methods: {
    removeTodo() {
      this.$emit("delete");
    },
    editTodo() {
      this.$emit("edit");
    },
  },
  updated() {
    this.$emit("isChecked", this.checkboxValue);
  },
};
</script>

<style scoped>
.listItem {
  padding: 10px;
  margin-top: 5px;
  margin-bottom: 5px;
}
.uncomplete {
  background-color: rgba(235, 122, 122, 0.408);
}
.complete {
  background-color: rgba(122, 235, 122, 0.408);
}
.inputField {
  display: flex;
  align-items: center;
  justify-content: flex-start;
}
.buttonField {
  display: flex;
  align-items: center;
  justify-content: right;
}
button {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-weight: bold;
  margin: 4px;
  padding: 8px;
  border-radius: 15px;
  border: none;
  width: 10%;
}
</style>