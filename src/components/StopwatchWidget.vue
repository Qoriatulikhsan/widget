<template>
  <div class="stopwatch-widget bg-gray-200 border border-gray-900 p-4 mb-4 h-full mt-40 ml-96 mr-96 rounded-xl">
    <h2 class="text-5xl font-bold mb-2">Stopwatch</h2>
    <p class="text-4xl text-gray-900 mb-2 mt-10">{{ formatTime }}</p>
    <div>
      <button @click="startStopwatch" :disabled="isRunning" class="py-2 px-4 bg-green-500 text-white rounded mr-2 mt-5 rounded-full">
        Start
      </button>
      <button @click="stopStopwatch" :disabled="!isRunning" class="py-2 px-4 bg-red-500 text-white rounded mr-2 mt-5 rounded-full">
        Stop
      </button>
      <button @click="resetStopwatch" class="py-2 px-4 bg-blue-500 text-white mt-5 rounded-full">
        Reset
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isRunning: false,
      startTime: null,
      elapsedTime: 0,
    };
  },
  computed: {
    formatTime() {
      const milliseconds = this.elapsedTime % 1000;
      const seconds = Math.floor(this.elapsedTime / 1000) % 60;
      const minutes = Math.floor(this.elapsedTime / 60000) % 60;
      const hours = Math.floor(this.elapsedTime / 3600000);

      return `${hours}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}:${milliseconds.toString().padStart(3, '0')}`;
    },
  },
  methods: {
    startStopwatch() {
      if (!this.isRunning) {
        this.isRunning = true;
        this.startTime = Date.now();

        this.timerInterval = setInterval(() => {
          this.elapsedTime = Date.now() - this.startTime;
        }, 10);
      }
    },
    stopStopwatch() {
      if (this.isRunning) {
        this.isRunning = false;
        clearInterval(this.timerInterval);
      }
    },
    resetStopwatch() {
      this.isRunning = false;
      clearInterval(this.timerInterval);
      this.elapsedTime = 0;
    },
  },
};
</script>



