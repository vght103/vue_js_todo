<template>
  <header class="header">
    <h1>todos</h1>
    <div class="relative">
      <input
        v-model="allChecked"
        @change="todoAllCompleted"
        id="toggle-all"
        class="toggle-all"
        type="checkbox"
      />
      <label for="toggle-all">Mark all as complete</label>

      <input
        v-model="newTodoInput"
        @keyup.enter="createTodo"
        class="new-todo"
        placeholder="What needs to be done?"
        autofocus=""
      />
    </div>
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
        console.log(this.newTodoInput);
        this.newTodoInput = "";
      }
    },
  },
};
</script>

<style scoped>
.relative {
  position: relative;
}
header input::-webkit-input-placeholder {
  font-style: italic;
  font-weight: 300;
  color: #e6e6e6;
}

header input::-moz-placeholder {
  font-style: italic;
  font-weight: 300;
  color: #e6e6e6;
}

header input::input-placeholder {
  font-style: italic;
  font-weight: 300;
  color: #e6e6e6;
}

header h1 {
  /* position: absolute; */
  /* top: -180px; */
  width: 100%;
  font-size: 100px;
  font-weight: 100;
  text-align: center;
  color: rgba(175, 47, 47, 0.15);
  -webkit-text-rendering: optimizeLegibility;
  -moz-text-rendering: optimizeLegibility;
  text-rendering: optimizeLegibility;
}

.new-todo,
.edit {
  position: relative;
  margin: 0;
  width: 100%;
  font-size: 24px;
  font-family: inherit;
  font-weight: inherit;
  line-height: 1.4em;
  border: 0;
  color: inherit;
  padding: 6px;
  border: 1px solid #999;
  box-shadow: inset 0 -1px 5px 0 rgba(0, 0, 0, 0.2);
  box-sizing: border-box;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.new-todo {
  padding: 16px 16px 16px 60px;
  border: none;
  background: rgba(0, 0, 0, 0.003);
  box-shadow: inset 0 -2px 1px rgba(0, 0, 0, 0.03);
}

.main {
  position: relative;
  z-index: 2;
  border-top: 1px solid #e6e6e6;
}

.toggle-all {
  width: 1px;
  height: 1px;
  border: none; /* Mobile Safari */
  opacity: 0;
  position: absolute;
  right: 100%;
  bottom: 100%;
}

.toggle-all + label {
  width: 60px;
  height: 34px;
  font-size: 0;
  position: absolute;
  top: 14px;
  left: 0;
  -webkit-transform: rotate(90deg);
  transform: rotate(90deg);
}

.toggle-all + label:before {
  content: "❯";
  font-size: 22px;
  color: #e6e6e6;
  padding: 10px 27px 10px 27px;
}

.toggle-all:checked + label:before {
  color: #737373;
}
</style>
