<template>
  <form class="todo-input" @submit.prevent="addNewTodo()">
    <input
      class="todo-input__input"
      id="todo-input"
      type="text"
      placeholder="Get sh*t done!"
      v-model="newToDo"
    />
    <button type="submit" class="todo-input__button button" id="add-button">
      Add
    </button>
  </form>
</template>

<script>
import { nanoid } from "nanoid";

export default {
  name: "AddTodoForm",
  emits: ["addToDo"],
  data() {
    return {
      newToDo: "",
    };
  },
  methods: {
    addNewTodo() {
      console.log(this.newToDo);

      const addedToDo = {
        id: nanoid(),
        description: this.newToDo,
        checked: false,
      };
      this.$emit("addToDo", addedToDo);
      /*
      if (!this.isToDoDouble && this.newToDo !== "") {
        this.todos.push({
          id: nanoid(),
          description: this.newToDo,
          checked: false,
        });
      }
      */
      this.newToDo = "";
    },
  },
};
</script>

<style scoped>
.todo-input {
  display: flex;
}

.todo-input .todo-input__input {
  margin-right: 1em;
}

.todo-input__input {
  all: unset;
  display: inline-block;
  flex-grow: 1;
  width: auto;
  background-color: white;
  padding: 0.5em;
  border: 0.1em solid transparent;
  border-radius: 0.3em;
}

.todo-input__input:focus {
  border: 0.1em solid var(--yellow);
}
</style>
