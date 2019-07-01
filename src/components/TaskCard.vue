<template>
  <vs-col
    class="colx"
    type="flex"
    vs-justify="space-around"
    vs-align="center"
    vs-lg="4"
    vs-sm="5"
    vs-xs="12"
  >
    <vs-row vs-justify="center">
      <vs-col type="flex" vs-justify="center" vs-align="center" vs-w="8">
        <vs-card>
          <div slot="header">
            <h3>
              {{ title }}
            </h3>
          </div>
          <div>
            {{ text }}
          </div>
          <div slot="footer">
            <vs-row vs-justify="flex-end">
              <vs-button color="danger" type="relief" @click="remove"
                >remove</vs-button
              >
            </vs-row>
          </div>
        </vs-card>
      </vs-col>
    </vs-row>
  </vs-col>
</template>

<script>
import log from "loglevel";

export default {
  name: "TaskCard",
  props: {
    id: {
      type: Number,
      required: true
    },
    title: {
      type: String,
      default: ""
    },
    text: {
      type: String,
      default: ""
    }
  },
  methods: {
    remove() {
      log.debug(`remove: ${this.id}`);
      this.$emit("remove-task", this.id);
    }
  }
};
</script>

<style></style>
