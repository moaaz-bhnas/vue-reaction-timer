<template>
  <h1>Reaction Timer</h1>

  <button
    type="button"
    class="playButton"
    @click="handlePlayClick"
    :disabled="buttonDisabled || blockVisible.visible"
  >
    play
  </button>

  <Block v-if="blockVisible.visible" @show-result="showResult" />

  <Result v-if="result" :result="result" />
</template>

<script>
import Block from "./components/Block.vue";
import Result from "./components/Result.vue";

function generateRandomDelay(maxSeconds = 4) {
  const msPerSecond = 1000;
  return Math.ceil(Math.random() * maxSeconds) * msPerSecond;
}

export default {
  name: "App",
  components: { Block, Result },
  data() {
    return {
      blockVisible: {
        visible: false,
        time: null,
      },
      result: null,
      buttonDisabled: false,
    };
  },
  methods: {
    handlePlayClick() {
      this.buttonDisabled = true;
      this.result = null;
      this.blockVisible.time = null;

      setTimeout(() => {
        this.buttonDisabled = false;
        this.blockVisible.visible = true;
        this.blockVisible.time = Date.now();
      }, generateRandomDelay(2));
    },
    showResult() {
      const result = Date.now() - this.blockVisible.time;
      this.result = result;
      this.blockVisible.visible = false;
    },
  },
  beforeCreate() {
    console.log(`the component is not yet created. You can't access the data`);
  },
  created() {
    console.log(`the component is  created. You can access the data`);
  },
  beforeMount() {
    console.log(`Not mounted to the DOM yet.`);
  },
  mounted() {
    console.log(`the component is now mounted to the DOM.`);
  },
  beforeUpdate() {
    console.log(`Data has changed, but UI not updated`);
  },
  updated() {
    console.log(`Data has changed, and UI updated`);
  },
  beforeUnmount() {
    console.log(`Before component is unmounted`);
  },
  unmounted() {
    console.log(`Component is unmounted`);
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;

  display: flex;
  flex-direction: column;
  align-items: center;

  --bg-green: #abfaaa;
}

.playButton {
  font-size: 1rem;
  padding: 0.75rem;
  cursor: pointer;
  background-color: var(--bg-green);
  border: none;
  border-radius: 0.5rem;
  margin-bottom: 1rem;
}

.playButton:disabled {
  cursor: not-allowed;
}
</style>
