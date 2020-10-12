<template>
  <section class="todoapp">
    <header class="header">
      <h1 class="title">Todo List</h1>
      <input
        type="text"
        class="new-todo"
        placeholder="Ajouter une nouvelle tache"
        v-model="newTodo"
        @keyup.enter="addToDo"
      />
    </header>
    <div class="main">
      <input  id="toggle-all" type="checkbox" class="toggle-all" v-model="allDone">
       <label for="toggle-all">Tout completer</label>
      <ul class="todo-list">
        <li
          class="todo"
          v-for="todo in filteredTodos"
          v-bind:key="todo.name"
          v-bind:class="{ completed: todo.completed, editing: todo ===  editing}"
        >
          <div class="view">
            <input type="checkbox" v-model="todo.completed" class="toggle">
            <label v-on:dblclick="editTodo(todo)"> {{ todo.name }} </label>
            <button class="destroy" v-on:click.prevent="deleteTodo(todo)"></button>
          </div>
          <input type="text" class="edit" v-model="todo.name" @keyup.enter="doneEdit">
        </li>
      </ul>
    </div>
    <footer class="footer" v-show="todos.length > 0">
      <span class="todo-count"
        ><strong> {{ remaining }}</strong> Tache à faire</span
      >
      <ul class="filters">
        <li>
          <a
            href="#"
            v-bind:class="{ selected: filter === 'all' }"
            @click.prevent="filter = 'all'"
            >Toutes</a>
        </li>
        <li>
          <a
            href="#"
            v-bind:class="{ selected: filter === 'todo' }"
            @click.prevent="filter = 'todo'"
            >A faire</a>
        </li>
        <li>
          <a
            href="#"
            v-bind:class="{ selected: filter === 'done' }"
            @click.prevent="filter = 'done'"
            >Réalisées</a>
        </li>
      </ul>
      <button class="clear-completed" v-show="completed" v-on:click='deleteCompleted'>Supprimer les taches réalisées</button>
    </footer>
  </section>
</template>

<style src="./todos.css">
.title {
  margin-top: 250px;
}
</style>

<script>
export default {
  data() {
    return {
      todos: [
        {
          name: "Faire la vaisselle",
          completed: false,
        },
      ],
      newTodo: "",
      filter: "all",
      editing: null,
    };
  },
  methods: {
    addToDo() {
      this.todos.push({
        name: this.newTodo,
        completed: false,
      });
      this.newTodo = "";
    },
    deleteTodo(todo) {
         this.todos = this.todos.filter(i => i !== todo)
    },
    deleteCompleted() {
        this.todos = this.todos.filter(todo => !todo.completed)
    },
    editTodo(todo) {
        this.editing = todo
    },
    doneEdit() {
        this.editing = null
    }
  },
  computed: {
    allDone: {
      get() {
       return this.remaining === 'O'
      },
      set(value) {
       if (value === true) {
           this.todos.forEach(todo => {
             return todo.completed = true
           })
       }
      },
    },
    remaining() {
      return this.todos.filter((todo) => !todo.completed).length;
    },
     completed() {
      return this.todos.filter((todo) => todo.completed).length;
    },

    filteredTodos() {
      if (this.filter === "todo") {
        return this.todos.filter((todo) => !todo.completed);
      } else if (this.filter === "done") {
        return this.todos.filter((todo) => todo.completed);
      }
      return this.todos;
    },
  },
};
</script>