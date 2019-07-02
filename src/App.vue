<template>
  <div id="app">
    <vs-navbar class="nabarx">
      <h1>
        <vs-navbar-title>Lovely Vue</vs-navbar-title>
      </h1>
    </vs-navbar>
    <vs-row vs-justify="center">
      <vs-input v-model="title" label="title" placeholder="Placeholder" />
      <vs-input v-model="text" label="text" placeholder="Placeholder" />
      <vs-button type="relief" :disabled="isDisabled" @click="add"
        >追加</vs-button
      >
    </vs-row>
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
import log from "loglevel";

export default {
  name: "App",
  components: {
    TaskCard
  },
  data: () => ({
    todos: [],
    title: "Title",
    text: "Text",
    keyLength: 0
  }),
  computed: {
    isDisabled() {
      return this.text.length === 0;
    }
  },
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
        log.debug(this.keyLength);
      } catch (e) {
        localStorage.removeItem("todos");
      }
    }
  },
  methods: {
    add() {
      log.debug(this.keyLength);
      this.keyLength++;
      const newTodo = {
        id: this.keyLength,
        title: this.title,
        text: this.text
      };
      this.todos.push(newTodo);
      this.title = "";
      this.text = "";
    },
    remove(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    }
  }
};
</script>

<style></style>
