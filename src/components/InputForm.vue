<template>
  <vs-row vs-justify="center">
    <vs-row vs-justify="center">
      <vs-input v-model="title" placeholder="title" class="input-margin" />
      <vs-input v-model="text" placeholder="text" class="input-margin" />
    </vs-row>
    <vs-row vs-justify="center">
      <vs-button
        type="relief"
        :disabled="isDisabled"
        class="input-margin"
        @click="add"
        >Add Task</vs-button
      >
    </vs-row>
  </vs-row>
</template>

<script>
export default {
  name: "InputForm",
  data: () => ({
    title: "",
    text: ""
  }),
  computed: {
    isDisabled() {
      return this.text.length === 0 || this.title.length === 0;
    }
  },
  methods: {
    add() {
      this.$emit("add-task", this.title, this.text);
      this.title = "";
      this.text = "";
    }
  }
};
</script>

<style>
.input-margin {
  margin: 10px 10px 0px 10px;
}
</style>
