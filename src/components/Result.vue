<template>
  <p>{{ rank }}</p>
</template>

<script>
export default {
  props: {
    result: Number,
  },
  computed: {
    rank() {
      return this.result < 250
        ? "Ninja Fingers"
        : this.result < 400
        ? "Rapid Reflexes"
        : "Snail Pace";
    },
  },
};
</script>
