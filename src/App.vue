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

export default {
  name: "App",
  components: {
    TaskCard
  },
  data: () => ({
    todos: [{ id: 1, title: "Task Title", text: "Task Text" }],
    title: "Title",
    text: "Text"
  }),
  computed: {
    isDisabled() {
      return this.text.length === 0;
    }
  },
  methods: {
    add() {
      const newTodo = {
        id: this.todos.length + 1,
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
