<template>
  <div class="stopwatch-area" :class="{ 'stopwatch-area__active': isRunning }">
    <p class="stopwatch-area__time">{{ getTime }}</p>
    <div class="stopwatch-area__controls">
      <control-button v-if="!isRunning" @click="startTimer">
        <svg width="17" height="20" viewBox="0 0 17 20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M0 20V0L17 10L0 20Z" :fill="getControlsColor"/>
        </svg>
      </control-button>

      <control-button v-else @click="pauseTimer">
        <svg width="10" height="20" viewBox="0 0 10 20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <rect x="7" width="3" height="20" fill="white"/>
          <rect width="3" height="20" fill="white"/>
        </svg>
      </control-button>

      <control-button @click="resetTimer">
        <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <rect width="20" height="20" :fill="getControlsColor"/>
        </svg>
      </control-button>
    </div>
  </div>  
</template>

<script>
import ControlButton from "./ControlButton.vue";

export default {
  components: { ControlButton },

  data() {
    return {
      seconds: 0,
      isRunning: false,
      interval: null,
    };
  },

   methods: {
    startTimer() {
      this.isRunning = true;

      this.interval = setInterval(() => {
        this.seconds++;
      }, 1000);
    },

    pauseTimer() {
      this.isRunning = false;
      clearInterval(this.interval);
    },

    resetTimer() {
      this.seconds = 0;
      this.isRunning = false;
      this.clearTimerInterval();
    },

    clearTimerInterval() {
      this.interval && clearInterval(this.interval);
    }
  },

  computed: {
    getTime() {
      const hours = Math.floor(this.seconds / 3600);
      const minutes = Math.floor((this.seconds - hours * 3600) / 60);
      const seconds = this.seconds - hours * 3600 - minutes * 60;

      return `${hours ? `${hours}:` : ''}${minutes ? `${minutes}:` : ''}${seconds}`
    },

    getControlsColor() {
      return this.isRunning ? 'white' : '#9E9E9E';
    }
  },

  beforeUnmount() {
    this.clearTimerInterval();
  },
};
</script>

<style scoped>
.stopwatch-area {
  height: 120px;
  background-color: #696969;
  font-weight: 400;
  font-size: 22px;
  line-height: 21px;
  font-family: 'Gotham Pro',sans-serif;
  text-align: center;
  color: #9E9E9E;
}

.stopwatch-area__time {
  padding: 22px 0 20px 0;
  margin: 0;
}

.stopwatch-area__controls {
  padding: 20px 0;
  display: flex;
  justify-content: center;
  gap: 50px;
  border-top: 1px solid #9E9E9E;
}

.stopwatch-area.stopwatch-area__active {
  color: white;
}

.stopwatch-area.stopwatch-area__active .stopwatch-area__controls {
  border-color: white;
}
</style>