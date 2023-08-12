<template>
  <header class="header">
    <h1 class="header__title">Todo App</h1>
  </header>
  <main class="main">
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

    <section class="filter-and-options">
      <h2>Filter & Options</h2>
      <div class="radio-container" id="radio-container">
        <input
          type="radio"
          name="filter"
          id="radio-all"
          value="all"
          class="radio-button"
          v-model="filterState"
          @change="filterToDos()"
          checked
        />
        <label for="radio-all">All</label>
        <input
          type="radio"
          name="filter"
          id="radio-open"
          value="open"
          class="radio-button"
          v-model="filterState"
          @change="filterToDos()"
        />
        <label for="radio-open">Open</label>
        <input
          type="radio"
          name="filter"
          id="radio-done"
          value="done"
          class="radio-button"
          v-model="filterState"
          @change="filterToDos()"
        />
        <label for="radio-done">Done</label>
      </div>
      <button class="button" id="delete-button">Remove Done Todos</button>
    </section>

    <section class="todos">
      <h2>Your Todos</h2>
      <ul class="todo-list" id="todo-list">
        <li class="todo-item" v-for="todo in filteredTodos" :key="todo.id">
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
    </section>
  </main>
</template>

<script>
import { nanoid } from "nanoid";

export default {
  name: "App",
  components: {},
  data() {
    return {
      todos: [
        {
          id: "x",
          description: "Learn HTML",
          checked: false,
        },
        {
          id: "y",
          description: "Learn CSS3",
          checked: false,
        },
        {
          id: "z",
          description: "Learn JavaScript",
          checked: false,
        },
      ],
      newToDo: "",
      filterState: "",
      filteredTodos: [],
    };
  },
  computed: {},
  mounted() {
    this.filteredTodos = this.todos;
  },
  methods: {
    addNewTodo() {
      console.log(this.newToDo);

      this.todos.push({
        id: nanoid(),
        description: this.newToDo,
        checked: false,
      });

      this.newToDo = "";
    },
    filterToDos() {
      console.log(this.filterState);
      if (this.filterState === "done") {
        this.filteredTodos = this.todos.filter((todo) => {
          return todo.checked === true;
        });
      } else if (this.filterState === "open") {
        this.filteredTodos = this.todos.filter((todo) => {
          return todo.checked === false;
        });
      } else {
        this.filteredTodos = this.todos;
      }
    },
  },
};
</script>

<style>
*,
*:before,
*:after {
  box-sizing: border-box;
}

html,
body {
  min-height: 100%;
}

html {
  font-size: 20px;
  font-family: sans-serif;

  --dark-blue: #073b4c;
  --light-blue: #118ab2;
  --green: #06d6a0;
  --yellow: #f5ab00;
  --pink: #ef476f;
}

h1,
h2 {
  margin: 0;
}

body {
  margin: 0;
  background-color: #f5f5f5;
}

.done {
  text-decoration: line-through;
}

.header {
  text-align: center;
  background-color: var(--pink);
  padding: 3rem 1rem;
  color: white;
  margin-bottom: 1rem;
}

.header__title {
  margin: 0;
  text-shadow: 2px 2px var(--light-blue), 4px 4px var(--yellow);
}

.button {
  all: unset;
  display: block;
  word-break: keep-all;
  word-wrap: normal;
  color: white;
  background-color: var(--light-blue);
  padding: 0.25em 0.4em;
  border-radius: 0.3em;
  border: 0.1em solid transparent;
  box-shadow: 3px 3px 0px var(--pink);
}

.button:focus {
  border: 0.1em solid var(--yellow);
}

.button:active {
  box-shadow: none;
}
.main {
  padding: 1rem;
  max-width: 35ch;
  margin: 0 auto;
}

.main > * + * {
  margin-top: 3rem;
}

.radio-button {
  all: unset;
  display: inline-block;
  flex-grow: 1;
  width: auto;
  background-color: white;
  padding: 0.5em;
  border: 0.1em solid var(--dark-blue);
  border-radius: 50%;
}

.radio-button:checked {
  background-color: var(--light-blue);
}

.radio-button:focus {
  border: 0.1em solid var(--yellow);
}

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

/* .filter-and-options {} */

.filter-and-options > * + * {
  margin-top: 1rem;
}

.radio-container {
  display: grid;
  grid-template-columns: auto 1fr;
  grid-gap: 0.5em 0.25em;
  align-items: center;
  justify-content: center;
}

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
