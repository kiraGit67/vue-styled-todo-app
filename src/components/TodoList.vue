<template>
  <ul class="todo-list" id="todo-list">
    <li class="todo-item" v-for="todo in todosList" :key="todo.id">
      <input
        class="todo-item__checkbox"
        type="checkbox"
        :name="todo.id"
        :id="todo.id"
        v-model="todo.checked"
      />
      <label class="todo-item__text" :for="todo.id">{{
        todo.description
      }}</label>
    </li>
  </ul>
</template>

<script>
export default {
  name: "TodoList",
  props: {
    todosList: Array,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todo-list {
  list-style-type: none;
  padding: 0;
}

.todo-list > * + * {
  margin-top: 0.5rem;
}

.todo-item {
  background-color: white;
  padding: 0.5em 1em;
  border-radius: 0.3em;
  display: flex;
  align-items: center;
  border: 0.1em solid transparent;
}

.todo-item:focus-within {
  box-shadow: 3px 3px 0 var(--pink);
  border: 0.1em solid var(--yellow);
}

.todo-item > .todo-item__checkbox {
  margin-right: 1em;
}

.todo-item__checkbox {
  all: unset;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 0.1em;
  width: 0.75em;
  height: 0.75em;
  border: 0.1em solid var(--dark-blue);
  background-color: white;
  background-size: 80% 80%;
  background-repeat: no-repeat;
  background-position: center center;
}

.todo-item__checkbox:checked {
  background-color: var(--green);
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' aria-hidden='true' focusable='false' %3E%3Cpath fill='none' stroke='white' stroke-width='3' d='M1.73 12.91l6.37 6.37L22.79 4.59' /%3E%3C/svg%3E");
}

.todo-item__text {
  flex-grow: 1;
}
</style>
