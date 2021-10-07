<template>
  <div>
    <p>{{ message.title }}</p>
  </div>
</template>

<script lang="ts">
import Vue, { PropType } from "vue";
import { ComplexMessage } from "./interface.Mycomponent"

const MyComponent= Vue.extend({
  props: {
    name: String,
    success: { type: String },
    callback: {
      type: Function as PropType<() => void>,
    },
    message: {
      type: Object as PropType <ComplexMessage>,
      required: true,
    },
  },
});


export default MyComponent
</script>

<style scoped></style>
