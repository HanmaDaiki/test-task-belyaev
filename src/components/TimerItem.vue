<template>
  <article class="timer">
    <h2 :class="start ? 'timer__display' : 'timer__display timer__disabled'">
      <span v-if="hours > 0">{{ hours }}:</span><span v-if="this.minutes > 0 || this.hours > 0">{{ minutes }}:</span>{{ seconds }}
    </h2>
    <div class="timer__controls">
      <button
        v-on:click="switchMode"
        :class="start ? 'timer__pause' : 'timer__start'"
      />
      <button
        v-on:click="stop"
        :class="start ? 'timer__stop' : 'timer__stop timer__disabled'"
      />
    </div>
  </article>
</template>

<script>
export default {
  name: 'TimerItem',
  data() {
    return {
      hours: this.timer.hours,
      minutes: this.timer.minutes,
      seconds: this.timer.seconds,
      start: false,
    };
  },
  methods: {
    switchMode() {
      this.start = this.start ? false : true;
      this.startTimer();
    },
    stop() {
      this.deleteTimer(this.timer.id);
    },
    startTimer() {
      if (this.start) {
        this.interval = setInterval(() => {
          if (this.hours > 0 && this.seconds === 0 && this.minutes === 0) {
            this.hours -= 1;
            this.minutes = 60;
          } else if (this.minutes > 0 && this.seconds === 0) {
            this.minutes -= 1;
            this.seconds = 60;
          } else if (this.seconds > 0) {
            this.seconds -= 1;
          }
        }, 1000);
      } else {
        clearInterval(this.interval);
      }
    },
  },
  props: {
    deleteTimer: Function,
    timer: Object,
  },
};
</script>

<style scoped>
.timer {
  box-sizing: border-box;
  padding: 22px 0 20px;
  width: 225px;
  height: 120px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  background-color: #696969;
}

.timer__display {
  margin: 0;
  width: 100%;
  text-align: center;
  font-weight: 400;
  font-size: 22px;
  line-height: 21px;
  padding-bottom: 20px;
  border-bottom: 1px solid #fff;
}

.timer__display.timer__disabled {
  color: #9e9e9e;
  border-color: #9e9e9e;
}

.timer__controls {
  display: flex;
  gap: 48px;
}

.timer__start {
  width: 17px;
  height: 20px;
  border: none;
  background-color: transparent;
  cursor: pointer;
  background-image: url(../assets/images/icon-start.svg);
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  transition: all 0.2s ease-in-out;
}

.timer__start:hover {
  transform: scale(1.1);
}

.timer__stop {
  width: 20px;
  height: 20px;
  background-color: #fff;
  border: none;
  transition: all 0.2s ease-in-out;
  cursor: pointer;
}

.timer__stop.timer__disabled {
  background-color: #9e9e9e;
}

.timer__stop:hover {
  transform: scale(1.1);
}

.timer__pause {
  width: 17px;
  height: 20px;
  border: none;
  background-color: transparent;
  cursor: pointer;
  background-image: url(../assets/images/icon-pause.svg);
  background-position: center;
  background-repeat: no-repeat;
  background-size: contain;
  transition: all 0.2s ease-in-out;
}

.timer__pause:hover {
  transform: scale(1.1);
}
</style>
