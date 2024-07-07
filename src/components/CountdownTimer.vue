<template>
  <div class="countdown-timer">
    <h1>Countdown Timer</h1>
    
    <div class="inputs">
      <input type="number" v-model.number="hours" placeholder="HH" min="0" />
      <input type="number" v-model.number="minutes" placeholder="MM" min="0" max="59" />
      <input type="number" v-model.number="seconds" placeholder="SS" min="0" max="59" />
    </div>

    <div class="controls">
      <button @click="startTimer">Start</button>
      <button @click="pauseTimer" :disabled="!isRunning">Pause</button>
      <button @click="resetTimer">Reset</button>
    </div>

    <div class="display">
      <span>{{ displayHours }}</span>:<span>{{ displayMinutes }}</span>:<span>{{ displaySeconds }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CountdownTimer',
  data() {
    return {
      hours: 0,
      minutes: 0,
      seconds: 0,
      remainingTime: 0,
      interval: null,
      isRunning: false
    };
  },
  computed: {
    displayHours() {
      return String(Math.floor(this.remainingTime / 3600)).padStart(2, '0');
    },
    displayMinutes() {
      return String(Math.floor((this.remainingTime % 3600) / 60)).padStart(2, '0');
    },
    displaySeconds() {
      return String(this.remainingTime % 60).padStart(2, '0');
    }
  },
  methods: {
    startTimer() {
      if (!this.isRunning) {
        this.remainingTime = (this.hours * 3600) + (this.minutes * 60) + this.seconds;
        if (this.interval) clearInterval(this.interval);
        this.interval = setInterval(() => {
          if (this.remainingTime > 0) {
            this.remainingTime--;
          } else {
            clearInterval(this.interval);
            this.isRunning = false;
            alert('Time is up!');
          }
        }, 1000);
        this.isRunning = true;
      }
    },
    pauseTimer() {
      if (this.isRunning) {
        clearInterval(this.interval);
        this.isRunning = false;
      }
    },
    resetTimer() {
      if (this.interval) clearInterval(this.interval);
      this.hours = 0;
      this.minutes = 0;
      this.seconds = 0;
      this.remainingTime = 0;
      this.isRunning = false;
    }
  }
};
</script>

<style scoped>
.countdown-timer {
  width: 300px;
  margin: 100px auto;
  text-align: center;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.inputs input {
  width: 60px;
  margin: 5px;
  padding: 5px;
  font-size: 16px;
  text-align: center;
}

.controls button {
  margin: 10px;
  padding: 10px 20px;
  font-size: 16px;
}

.display {
  font-size: 32px;
  margin-top: 20px;
}
</style>
