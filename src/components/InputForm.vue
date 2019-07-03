<template>
  <div class="f-center">
    <vs-button color="primary" type="filled" @click="active = true"
      >Create Task Card</vs-button
    >
    <vs-popup
      class-content="popup-example"
      title="Create Task Card"
      :active.sync="active"
    >
      <vs-input v-model="title" placeholder="title" />
      <vs-input v-model="text" placeholder="text" />
      <vs-button type="relief" :disabled="isDisabled" @click="add"
        >Add Task</vs-button
      >
    </vs-popup>
  </div>
</template>

<script>
export default {
  name: "InputForm",
  data: () => ({
    title: "",
    text: "",
    active: false
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
      this.active = false;
    }
  }
};
</script>

<style>
.f-center {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  margin-top: 24px;
}

.vs-input {
  margin: 8px auto;
}

.vs-button {
  display: block;
  margin: 8px auto;
}
</style>
