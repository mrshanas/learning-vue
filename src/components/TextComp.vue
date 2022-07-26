<template>
  <h1>{{ this.msg }}</h1>
  <slot>If no slot is passed</slot>
</template>

<script>
export default {
  props: {
    msg: String,
  },
  emits: ["response"],
  mounted() {
    this.$emit("response", "Yay am emitted");
  },
};
</script>
