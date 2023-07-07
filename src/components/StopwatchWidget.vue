<template>
    <div class="stopwatch-widget">
      <h2>Stopwatch</h2>
      <p>{{ formatTime }}</p>
      <div>
        <button class="start" @click="startStopwatch" :disabled="isRunning">Start</button>
        <button class="stop" @click="stopStopwatch" :disabled="!isRunning">Stop</button>
        <button class="reset" @click="resetStopwatch">Reset</button>
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
  
  <style scoped>
  .stopwatch-widget {
    border: 1px solid #ccc;
    padding: 20px;
    margin-bottom: 20px;
  }
  
  .stopwatch-widget h2 {
    color: #333;
    font-size: 24px;
    margin-bottom: 10px;
  }
  
  .stopwatch-widget p {
    color: #666;
    font-size: 25px;
    margin-bottom: 20px;
    font-family: 'digital';
  }
  
  .stopwatch-widget button {
    padding: 10px 20px;
    background-color: #4caf50;
    color: white;
    border: none;
    border-radius: 4px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .stopwatch-widget button.stop {
    background-color: #f60000;
    color: white;
  }
  .stopwatch-widget button.reset {
    background-color: #0062f6;
    color: white;
  }
  .stopwatch-widget button:hover {
    background-color: #45a049;
  }
  .stopwatch-widget button.stop:hover {
    background-color: #dc0303;
    color: white;
  }
  .stopwatch-widget button.reset:hover {
    background-color: #0452c8;
    color: white;
  }
  
  .stopwatch-widget button:disabled {
    background-color: #ccc;
    color: #999;
    cursor: not-allowed;
  }
  .stopwatch-widget button.stop:disabled {
    background-color: #ccc;
    color: #999;
    cursor: not-allowed;
  }
  </style>