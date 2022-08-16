<template>
  <h1>Reaction Timer</h1>

  <button
    type="button"
    class="playButton"
    @click="handlePlayClick"
    :disabled="buttonDisabled"
  >
    play
  </button>

  <Block v-if="blockVisible" @show-result="showResult" />

  <Result :result="clickTime" />
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
      blockVisible: false,
      blockVisiblityTime: null,
      resultVisible: false,
      buttonDisabled: false,
      clickTime: null,
    };
  },
  methods: {
    handlePlayClick() {
      this.buttonDisabled = true;
      this.resultVisible = false;
      this.clickTime = null;
      this.blockVisiblityTime = null;

      setTimeout(() => {
        this.buttonDisabled = false;
        this.blockVisible = true;
        this.blockVisiblityTime = Date.now();
      }, generateRandomDelay(2));
    },
    showResult() {
      const clickTime = Date.now() - this.blockVisiblityTime;
      this.clickTime = clickTime;
      this.blockVisible = false;
      this.resultVisible = true;
    },
  },
  // computed: {
  //   result() {
  //     console.log({
  //       "Date.now()": Date.now(),
  //       "this.blockVisiblityTime": this.blockVisiblityTime,
  //     });
  //     return Date.now() - this.blockVisiblityTime;
  //   },
  // },
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
