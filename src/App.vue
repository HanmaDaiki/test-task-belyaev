<template>
  <div class="container">
    <TimerItem
      v-bind:deleteTimer="deleteTimer"
      v-bind:timer="timer"
      v-for="timer in timers"
      :key="timer.id"
    />
    <TimerCreationForm v-bind:addNewTimer="addNewTimer" v-if="this.create"/>
    <button v-on:click="() => this.create = true" class="create-timer" v-else />
  </div>
</template>

<script>
import TimerItem from './components/TimerItem.vue';
import TimerCreationForm from './components/TimerCreationForm.vue';

export default {
  name: 'App',
  components: {
    TimerItem,
    TimerCreationForm
},
  data() {
    return {
      timers: [],
      create: false,
    };
  },
  methods: {
    addNewTimer(hours, minutes, seconds) {
      this.timers.push({
        id: Date.now(),
        hours: hours,
        minutes: minutes,
        seconds: seconds,
      });
      this.create = false
    },
    deleteTimer(id) {
      this.timers = this.timers.filter((timer) => timer.id !== id);
    },
  },
};
</script>

<style>
@import '~normalize.css/normalize.css';

@font-face {
  font-family: 'GothamPro';
  src: url(./vendor/fonts/GothamPro.woff) format('woff');
  src: url(./vendor/fonts/GothamPro.ttf) format('truetype');
  font-weight: 400;
}

body {
  font-family: 'GothamPro';
  font-weight: 400;
  background-color: #353638;
  color: #fff;
}

.container {
  padding: 72px 46px;
  display: flex;
  gap: 45px;
  flex-direction: column;
  align-items: center;
}

.create-timer {
  width: 225px;
  height: 120px;
  background-color: #696969;
  border: none;
  cursor: pointer;
  background-image: url(./assets/images/icon-add.svg);
  background-position: center;
  background-size: 20px 20px;
  background-repeat: no-repeat;
  transition: all 0.2s ease-in-out;
}

.create-timer:hover {
  background-size: 25px 25px;
}

@media screen and (min-width: 768px) {
  .container {
    padding: 72px 135px;
    flex-direction: row;
    flex-wrap: wrap;
  }
}

@media screen and (min-width: 1024px) {
  .container {
    padding: 72px 212px;
    gap: 50px;
  }
}
</style>
