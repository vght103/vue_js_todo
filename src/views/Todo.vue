<template>
  <section class="todoapp">
    <Header @create-todo="createTodo" />
    <section class="main">
      <ul :class="'todo-list ' + status">
        <li
          v-for="todo in todos"
          :key="todo.id"
          :class="{ completed: todo.completed, editing: todo.edit }"
        >
          <div class="view">
            <input
              v-model="todo.completed"
              @change="todoAllCompletedAction(todo)"
              class="toggle"
              type="checkbox"
            />
            <label @dblclick="updateTodoAction(todo)">{{ todo.title }}</label>
            <button @click="deleteTodo(todo)" class="destroy"></button>
          </div>
          <input
            v-model="todo.title"
            @blur="todo.edit = false"
            @keyup.enter="updateTodo(todo)"
            class="edit"
          />
        </li>
      </ul>
    </section>
    <Footer
      :todosItems="todos"
      :is-show="todos.length > 0"
      @update-status="updateStatus"
      @clear-completed="clearCompleted"
    />
  </section>
</template>

<script>
import Header from "../components/Header.vue";
// import Footer from "../components/Footer.vue";

import axios from "axios";

export default {
  components: {
    Header,
    // Footer,
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
    this.getTodos();
    // this.todos = JSON.parse(localStorage.getItem("todosData"));
  },

  methods: {
    async getTodos() {
      var tokenInfo = localStorage.getItem("token");
      if (tokenInfo) {
        var response = await axios({
          url: "http://149.28.19.152:7500/todos",
          method: "GET",
          headers: {
            authorization: "Bearer " + tokenInfo,
          },
        });

        if (response.data) {
          this.todos = response.data;
        }
      }
    },
    async createTodo(todoText) {
      //api call
      var tokenInfo = localStorage.getItem("token");
      if (tokenInfo) {
        var response = await axios({
          url: "http://149.28.19.152:7500/todo",
          method: "POST",
          data: {
            title: todoText,
          },
          headers: {
            authorization: "Bearer " + tokenInfo,
          },
        });
        console.log(response.data);
      }

      if (response.data) {
        var newTodo = response.data;
        newTodo.edit = false;
        this.todos.push(newTodo);
        // this.todos.push({
        //   id: new Date().getTime(),
        //   title: todoText,
        //   completed: false,
        //   edit: false,
        // });
        console.log(this.todos);
      }
    },

    async deleteTodo(todo) {
      var tokenInfo = localStorage.getItem("token");
      if (tokenInfo) {
        var response = await axios({
          url: "http://149.28.19.152:7500/todo/ " + todo.id,
          method: "DELETE",

          headers: {
            authorization: "Bearer " + tokenInfo,
          },
        });
      }

      if (response.data) {
        var todoIdx = this.todos.indexOf(todo);
        if (todoIdx > -1) {
          this.todos.splice(todoIdx, 1);
        }
      }
    },

    todoAllCompletedAction() {
      this.allChecked = this.todos.every((todo) => todo.completed);
    },

    todoAllCompleted() {
      this.todos.forEach((todo) => (todo.completed = this.allChecked));
    },

    updateTodoAction(todo) {
      todo.edit = true;

      console.log(todo.edit);
    },

    async updateTodo(todo) {
      var tokenInfo = localStorage.getItem("token");

      if (tokenInfo) {
        var response = await axios({
          url: "http://149.28.19.152:7500/todos",
          method: "PUT",

          headers: {
            authorization: "Bearer" + tokenInfo,
          },
        });
      }

      if (response.data) {
        todo.edit = false;
      }
    },

    updateStatus(status) {
      this.status = status;
      console.log(this.status);
    },

    clearCompleted() {
      // todo.completed == true 삭제
      var activeTodos = this.todos.filter((todo) => todo.completed == false);

      this.todos = activeTodos;
    },

    saveTodos() {
      localStorage.setItem("todosData", JSON.stringify(this.todos));
    },
  },
};
</script>

<style scoped>
.todoapp {
  background: #fff;
  margin: 130px 0 40px 0;
  position: relative;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);
}

.todo-list {
  margin: 0;
  padding: 0;
  list-style: none;
}

.todo-list li {
  position: relative;
  font-size: 24px;
  border-bottom: 1px solid #ededed;
}
.todo-list li input.edit {
  display: none;
}

.todo-list li:last-child {
  border-bottom: none;
}

.todo-list li.editing {
  border-bottom: none;
  padding: 0;
}

.todo-list li.editing .edit {
  display: block;
  width: 506px;
  padding: 12px 16px;
  margin: 0 0 0 43px;
}

.todo-list li.editing .view {
  display: none;
}
.todo-list li.editing input {
  display: inline-block;
}

.todo-list li .toggle {
  text-align: center;
  width: 40px;
  height: auto;
  position: absolute;
  top: 0;
  bottom: 0;
  margin: auto 0;
  border: none;
  -webkit-appearance: none;
  appearance: none;
}

.todo-list li .toggle {
  opacity: 0;
}

.todo-list li .toggle + label {
  background-image: url("data:image/svg+xml;utf8,%3Csvg%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%20width%3D%2240%22%20height%3D%2240%22%20viewBox%3D%22-10%20-18%20100%20135%22%3E%3Ccircle%20cx%3D%2250%22%20cy%3D%2250%22%20r%3D%2250%22%20fill%3D%22none%22%20stroke%3D%22%23ededed%22%20stroke-width%3D%223%22/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: center left;
}

.todo-list li .toggle:checked + label {
  background-image: url("data:image/svg+xml;utf8,%3Csvg%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%20width%3D%2240%22%20height%3D%2240%22%20viewBox%3D%22-10%20-18%20100%20135%22%3E%3Ccircle%20cx%3D%2250%22%20cy%3D%2250%22%20r%3D%2250%22%20fill%3D%22none%22%20stroke%3D%22%23bddad5%22%20stroke-width%3D%223%22/%3E%3Cpath%20fill%3D%22%235dc2af%22%20d%3D%22M72%2025L42%2071%2027%2056l-4%204%2020%2020%2034-52z%22/%3E%3C/svg%3E");
}

.todo-list li label {
  word-break: break-all;
  padding: 15px 15px 15px 60px;
  display: block;
  line-height: 1.2;
  transition: color 0.4s;
}

.todo-list li.completed label {
  color: #d9d9d9;
  text-decoration: line-through;
}

.todo-list li .destroy {
  display: none;
  position: absolute;
  top: 0;
  right: 10px;
  bottom: 0;
  width: 40px;
  height: 40px;
  margin: auto 0;
  font-size: 30px;
  color: #cc9a9a;
  margin-bottom: 11px;
  transition: color 0.2s ease-out;
}

.todo-list li .destroy:hover {
  color: #af5b5e;
}

.todo-list li .destroy:after {
  content: "×";
}

.todo-list li:hover .destroy {
  display: block;
}

.todo-list li .edit {
  display: none;
}

.todo-list li.editing:last-child {
  margin-bottom: -1px;
}
</style>
