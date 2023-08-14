<template>
  <todo-header :headerTitle="headerTitle" />
  <main class="main">
    <add-todo-form @addToDo="addNewTodo" />
    <!--
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
    -->
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
      <delete-button
        :buttonText="deleteButtonText"
        @deleteToDo="removeDoneToDos()"
      />
      <!--
      <button class="button" id="delete-button">Remove Done Todos</button>
      -->
    </section>

    <section class="todos">
      <h2>Your Todos</h2>
      <todo-list :todosList="filteredTodos" />
      <!--
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
      -->
    </section>
  </main>
</template>

<script>
import TodoHeader from "@/components/TodoHeader.vue";
import AddTodoForm from "@/components/AddTodoForm.vue";
import TodoList from "@/components/TodoList.vue";
import DeleteButton from "@/components/DeleteButton.vue";

export default {
  name: "App",
  components: {
    TodoHeader,
    AddTodoForm,
    TodoList,
    DeleteButton,
  },
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
      filterState: "",
      filteredTodos: [],
      headerTitle: "ToDo APP",
      deleteButtonText: "Remove Done ToDo's",
    };
  },
  mounted() {
    this.filteredTodos = this.todos;
  },
  methods: {
    isToDoDouble(item) {
      return this.todos
        .map((todo) => {
          return todo.description;
        })
        .includes(item);
    },
    addNewTodo(addedToDo) {
      if (
        addedToDo.description !== "" &&
        !this.isToDoDouble(addedToDo.description)
      ) {
        this.todos.push(addedToDo);
      }
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
    removeDoneToDos() {
      this.todos = this.todos.filter((todo) => {
        return todo.checked === false;
      });
      this.filteredTodos = this.todos;
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
/**/
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
</style>
