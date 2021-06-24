<template>
  <footer class="footer" v-show="isShow">
    <span class="todo-count"></span>
    <ul class="filters">
      <li>
        <a href="#/" class="list-all">All</a>
      </li>
      <li>
        <a href="#/active" class="list-active">Active</a>
      </li>
      <li>
        <a href="#/completed" class="list-completed">Completed</a>
      </li>
    </ul>
    <button class="clear-completed">Clear completed</button>
  </footer>
</template>

<script>
export default {
  name: "footer",
  props: {
    isShow: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style></style>
