<template>
  <div id="app">
    <vs-navbar class="nabarx">
      <div slot="title">
        <vs-navbar-title><h1>Task App</h1></vs-navbar-title>
      </div>
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
import axios from "axios";

export default {
  name: "App",
  components: {
    TaskCard,
    InputForm
  },
  data: () => ({
    todos: []
  }),
  mounted() {
    axios.get(`http://localhost:8890/api/tasks`).then(res => {
      this.todos = res.data.data;
    });
  },
  methods: {
    add(title, text) {
      axios
        .post(`http://localhost:8890/api/tasks`, {
          title: title,
          text: text
        })
        .then(res => {
          this.todos.push(res.data.data);
        });
    },
    remove(id) {
      axios.delete("http://localhost:8890/api/tasks/" + id);
      this.todos = this.todos.filter(todo => todo.id !== id);
    }
  }
};
</script>

<style></style>
