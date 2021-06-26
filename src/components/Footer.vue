<template>
  <footer class="footer" v-show="isShow">
    <span class="todo-count">{{ activeTodosCount }} left items</span>

    <ul class="filters">
      <li>
        <a href="#/" class="list-all" @click="updateStatus('')">All</a>
      </li>
      <li>
        <a href="#/active" class="list-active" @click="updateStatus('active')"
          >Active</a
        >
      </li>
      <li>
        <a
          href="#/completed"
          class="list-completed"
          @click="updateStatus('completed')"
          >Completed</a
        >
      </li>
    </ul>
    <button @click="clearCompleted" class="clear-completed">
      Clear completed
    </button>
  </footer>
</template>

<script>
export default {
  props: {
    todoItems: {
      type: Array,
      required: true,
    },
    isShow: {
      type: Boolean,
      default: false,
    },
  },
  computed: {
    activeTodosCount() {
      // [{id: '',}, {}]
      var activeTodos = this.todoItems.filter((todo) => {
        return !todo.completed;
      });
      return activeTodos.length;
      //return this.todoItems.filter(todo => !todo.completed).length;
    },
  },
  methods: {
    updateStatus(status) {
      this.$emit("updateStatus", status);
      console.log(status);
    },

    clearCompleted() {
      this.$emit("clearComplete");
      console.log(this.$emit("clearComplete"));
    },
  },
};
</script>

<style></style>
