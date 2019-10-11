<template>
  <div>
    <h2>Todo application</h2>

    <AddTodo @add-todo="addTodo" />

    <Todolist v-bind:todos="todos" v-on:remove-todo="removeTodo" v-on:add-todo="addTodo" />
  </div>
</template>



<script>
import Todolist from "@/components/Todolist.vue";
import AddTodo from "@/components/AddTodo.vue";

export default {
  name: "app",

  data() {
    return {
      todos: []
    };
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then(response => response.json())
      .then(json => {
        this.todos = json;
      });
  },

  components: {
    Todolist,
    AddTodo
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