<template>
  <section class="todoapp">
    <Header @create-todo="createTodo" />
    <section class="main">
      <input
        v-model="allChecked"
        @change="todoAllCompleted"
        id="toggle-all"
        class="toggle-all"
        type="checkbox"
      />
      <label for="toggle-all">Mark all as complete</label>
      <ul class="todo-list">
        <li
          v-for="todo in todos"
          :key="todo.id"
          :class="{ completed: todo.completed, editing: todo.edit }"
        >
          <div class="view">
            <input
              v-model="todo.completed"
              @change="todoCompleted"
              class="toggle"
              type="checkbox"
            />
            <label @dblclick="updateTodoAction(todo)">{{ todo.text }}</label>
            <button @click="deleteTodo(todo)" class="destroy"></button>
          </div>
          <input
            v-model="todo.text"
            @keyup.enter="updateTodo(todo)"
            @blur="todo.edit = false"
            class="edit"
          />
        </li>
      </ul>
    </section>
    <Footer
      @clear-completed="clearCompleted"
      @update-status="updateStatus"
      :isShow="this.todos.length > 0"
      :todoItems="todos"
    />
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
      status: "",
      todos: [],
      allChecked: false,
    };
  },

  watch: {
    todos: {
      deep: true,
      handler() {
        this.saveTodos();
      },
    },
  },

  mounted() {
    this.todos = JSON.parse(localStorage.getItem("todos"));
  },

  methods: {
    createTodo(todoText) {
      this.todos.push({
        // todo
        id: new Date().getTime(),
        text: todoText,
        completed: false,
        edit: false,
      });
    },

    deleteTodo(todo) {
      var todoIdx = this.todos.indexOf(todo);
      this.todos.splice(todoIdx, 1);
    },

    todoCompleted() {
      this.allChecked = this.todos.every((todo) => todo.completed);
    },

    todoAllCompleted() {
      this.todos.forEach((todo) => (todo.completed = this.allChecked));
      console.log(this.allChecked);
    },

    updateTodoAction(todo) {
      todo.edit = true;
    },

    updateTodo(todo) {
      todo.edit = false;
    },

    updateStatus(status) {
      this.status = status;
      console.log(status);
    },

    clearCompleted() {
      var activeTodos = this.todos.filter((todo) => {
        return todo.completed == false;
      });
      this.todos = activeTodos;
    },

    saveTodos() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
};
</script>

<style></style>
