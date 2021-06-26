<template>
  <header class="header">
    <h1>todos</h1>
    <input
      v-model="newTodoInput"
      @keyup.enter="createTodo"
      class="new-todo"
      placeholder="What needs to be done?"
      autofocus=""
    />
  </header>
</template>

<script>
export default {
  data() {
    return {
      newTodoInput: "",
    };
  },

  methods: {
    createTodo() {
      if (this.newTodoInput) {
        this.$emit("createTodo", this.newTodoInput);
        this.newTodoInput = "";
      }
    },
  },
};
</script>

<style>
h1 {
  /* margin-bottom: 50px; */
}
</style>
