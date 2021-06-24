<template>
  <section class="todoapp">
    <section class="main">
      <Header @create-todo="createTodo" />
      <input id="toggle-all" class="toggle-all" type="checkbox" />
      <label for="toggle-all">Mark all as complete</label>
      <ul class="todo-list">
        <li v-for="todo in todos" :key="todo.id">
          <div class="view">
            <input class="toggle" type="checkbox" />
            <label>{{ todo.text }}</label>
            <button class="destroy"></button>
          </div>
          <input class="edit" />
        </li>
      </ul>
    </section>
    <Footer />
  </section>
</template>

<script>
import Header from "../components/Header.vue";
import Footer from "../components/Footer.vue";

export default {
  components: {
    Header,
    Footer,
  },

  data() {
    return {
      todos: [],
    };
  },

  methods: {
    createTodo(todoText) {
      this.todos.push({
        id: new Date().getTime(),
        text: todoText,
        completed: false,
        edit: false,
      });
      console.log(this.todos);
    },
  },
};
</script>

<style></style>
