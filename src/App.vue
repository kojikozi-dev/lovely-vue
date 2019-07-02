<template>
  <div id="app">
    <vs-navbar class="nabarx">
      <h1>
        <vs-navbar-title>Lovely Vue</vs-navbar-title>
      </h1>
    </vs-navbar>
    <InputForm @add-task="add" />
    <br />
    <template v-if="todos.length === 0">
      タスクはありません
    </template>
    <template v-else>
      <vs-row class="wrap" vs-type="flex" vs-justify="flex-start">
        <TaskCard
          v-for="todo in todos"
          :id="todo.id"
          :key="todo.id"
          :title="todo.title"
          :text="todo.text"
          @remove-task="remove"
        />
      </vs-row>
    </template>
  </div>
</template>

<script>
import TaskCard from "@/components/TaskCard.vue";
import InputForm from "@/components/InputForm.vue";

export default {
  name: "App",
  components: {
    TaskCard,
    InputForm
  },
  data: () => ({
    todos: [],
    keyLength: 0
  }),
  watch: {
    todos: {
      handler: function(todos) {
        localStorage.setItem("todos", JSON.stringify(todos));
        localStorage.keylength = todos.length;
      },
      deep: true
    }
  },
  mounted() {
    if (localStorage.getItem("todos")) {
      try {
        this.todos = JSON.parse(localStorage.getItem("todos"));
        this.todos.forEach(function(todo, index) {
          todo.id = index + 1;
        });
        this.keyLength = Number(localStorage.keylength);
      } catch (e) {
        localStorage.removeItem("todos");
      }
    }
  },
  methods: {
    add(title, text) {
      this.keyLength++;
      const newTodo = {
        id: this.keyLength,
        title: title,
        text: text
      };
      this.todos.push(newTodo);
    },
    remove(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    }
  }
};
</script>

<style></style>
