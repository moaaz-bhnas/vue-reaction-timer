<template>
  <button class="button" type="button" @click="showResult">Click me!</button>
</template>

<script>
export default {
  methods: {
    showResult() {
      this.$emit("show-result");
    },
  },
};
</script>

<style scoped>
.button {
  padding: 8rem;
  cursor: pointer;
  border: none;
  border-radius: 0.5rem;
  background-color: var(--bg-green);
}
</style>
