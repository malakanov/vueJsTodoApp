<template>
  <div>
    <h2>Todo application</h2>

    <AddTodo @add-todo="addTodo" />
    <select v-model="filter">
<option value="all">All</option>
<option value="completed">Completed</option>
<option value="not-completed">Not-completed</option>

    </select>

    <Loader v-if="loading" />

    <Todolist
      v-else-if="todos.length"
      v-bind:todos="filteredTodos"
      v-on:remove-todo="removeTodo"
      v-on:add-todo="addTodo"
    />
    
    <a href="/">Home</a>
  </div>
</template>



<script>
import Todolist from "@/components/Todolist.vue";
import AddTodo from "@/components/AddTodo.vue";
import Loader from "@/components/Loader.vue";

export default {
  name: "app",

  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    };
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then(response => response.json())
      .then(json => {
        setTimeout(() => {
          this.todos = json;
          this.loading = false;
        }),
          1000;
      });
  },

computed: {
  filteredTodos() {
    if (this.filter === 'all'){
      return this.todos
    }
    if (this.filter === 'completed'){
      return this.todos.filter(t => t.completed )
    }
    if (this.filter === 'not-completed'){
      return this.todos.filter(t => !t.completed )
    }
  }
},

  components: {
    Todolist,
    AddTodo,
    Loader
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(item => item.id !== id);
    },
    addTodo(todo) {
      this.todos.push(todo);
    }
  }
};
</script>