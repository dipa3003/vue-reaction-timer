<template>
  <h1>Vue Reaction Timer</h1>
  <p>Ninja Fingers: Very good!, Rapid Reflexes: Good!, Snail Pace: Too slow!</p>
  <button @click="start" :disabled="isPlaying">Play</button>
  <Block v-if="isPlaying" :delay="delay" @reactionTime="endGame"></Block>
  <Result v-if="showReaction" :score="score" />
</template>

<script>
import Block from "./components/Block.vue";
import Result from "./components/Result.vue";

export default {
  name: "App",
  components: {
    Block,
    Result,
  },
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showReaction: false,
    };
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000;
      this.isPlaying = true;
      this.showReaction = false;
    },
    endGame(reactionTime) {
      this.score = reactionTime;
      this.isPlaying = false;
      this.showReaction = true;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}
button {
  background: #0faf87;
  color: white;
  border: none;
  margin: 10px;
  padding: 8px 16px;
  font-size: 16px;
  letter-spacing: 1px;
  border-radius: 4px;
  cursor: pointer;
}
button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}
</style>
