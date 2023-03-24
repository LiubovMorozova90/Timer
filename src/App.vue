<template>
  <div class="container">
    <div class="timer-app">
      <stopwatch v-for="(_, index) in stopwatches" :key="index" />

      <div class="timer-app__add-timer" @click="addStopwatch">
        <control-button>
          <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <rect x="8.3" width="3" height="20" fill="#9E9E9E"/>
            <rect y="3.5" x="-8" width="3" height="20" transform="rotate(-90 0 3.5)" fill="#9E9E9E"/>
          </svg>
        </control-button>
      </div>    
    </div>
  </div>
</template>

<script>
import Stopwatch from './components/Stopwatch.vue';
import ControlButton from "./components/ControlButton.vue";

export default {
  components: {
    ControlButton,
    Stopwatch,
  },

  data() {
    return {
      stopwatches: []
    };
  },

  methods: {
    addStopwatch() {
      this.stopwatches.push({});
    }
  }
};
</script>

<style scoped>
.container {
  min-height: 100vh;
  background-color: #353638;
  display: flex;
  align-items: center;
  justify-content: center;
}

.timer-app {
  max-width: 780px;
  width: 100%;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(225px, 225px));
  justify-content: center;
  column-gap: 50px;
  row-gap: 45px;
}

.timer-app__add-timer {
  height: 120px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #696969;
  cursor: pointer;
}
</style>
