<template>
    <h1>Ninja Reaction Timer</h1>
    <button @click="start" :disabled="isPlaying">Play</button>
    <Block v-if="isPlaying" :delay="delay" @end="endGame" />
    <p v-if="isPlaying && !showResults">Wait for it...</p>
    <Results v-if="showResults" :score="score" />
</template>

<script>
import Block from './components/Block.vue'
import Results from './components/Results.vue'

export default {
  name: 'App',
  components: { Block, Results },
  data() {
    return {
            isPlaying: false,
            delay: null,
            score: null,
            showResults: false
        }
  },
  methods: {
      start() {
          // Base time 2000 ms, Added to random number from 0 to 1 multiplied by 5000 ms
          // Max time is 7000ms, effective time range is 2000 - 7000 ms
          this.delay = 500 + Math.random() * 1500
          this.isPlaying = true
          this.showResults = false
      },
      endGame(reactionTime) {
          this.score = reactionTime
          this.isPlaying = false
          this.showResults = true
      }
  },
}
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
    padding: 8px 16px;
    border-radius: 4px;
    font-size: 16px;
    letter-spacing: 1px;
    cursor: pointer;
    margin: 10px;
}
button[disabled] {
    opacity: 0.2;
    cursor: not-allowed;
}
</style>
