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
  name: "header",

  data() {
    return {
      newTodoInput: null,
    };
  },

  methods: {
    createTodo() {
      if (this.newTodoInput) {
        this.$emit("createTodo", this.newTodoInput);

        this.newTodoInput = null;
      }
    },
  },
};
</script>

<style></style>
