<template>
  <footer class="footer" v-show="isShow">
    <span class="todo-count">{{ activeTodoCount }} left items</span>

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
    <button class="clear-completed" @click="clearCompleted">
      Clear completed
    </button>
  </footer>
</template>

<script>
export default {
  props: {
    todosItems: {
      type: Array,
      required: true,
    },

    isShow: {
      type: Boolean,
      default: false,
    },
  },

  computed: {
    activeTodoCount() {
      var activeTodos = this.todosItems.filter((todo) => {
        return todo.completed == false;
      });
      return activeTodos.length;
    },
  },

  methods: {
    updateStatus(status) {
      this.$emit("updateStatus", status);
      console.log(status);
    },

    clearCompleted() {
      this.$emit("clearCompleted");
    },
  },
};
</script>

<style></style>
