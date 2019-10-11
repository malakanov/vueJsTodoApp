<template>
  <form @submit.prevent="onSubmit">
    <input type v-model="title" />
    <button type="submit">Create</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: ""
    };
  },

  methods: {
    onSubmit() {
      let newTodo = {
        id: Date.now(),
        title: this.title,
        completed: false
      };
      this.$emit("add-todo", newTodo);
      this.title = "";
    }
  }
};
</script>

<style scoped>
form {
  display: flex;
}
input {
  width: 400px;
}
</style>
