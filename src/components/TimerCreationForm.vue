<template>
  <form class="timer-creation-form" @submit.prevent="() => addNewTimer(this.hours, this.minutes, this.seconds)">
    <input
      @input="hours = $event.target.value"
      class="timer-creation-form__input"
      v-bind:value="hours"
      placeholder="Часы"
      type="number"
      v-bind:min="0"
      v-bind:max="999"
    />
    <input
      @input="minutes = $event.target.value"
      class="timer-creation-form__input"
      v-bind:value="minutes"
      placeholder="Минуты"
      type="number"
      v-bind:min="0"
      v-bind:max="60"
    />
    <input
      @input="seconds = $event.target.value"
      class="timer-creation-form__input"
      v-bind:value="seconds"
      placeholder="Секунды"
      type="number"
      v-bind:min="0"
      v-bind:max="60"
    />
    <button type="submit" class="timer-creation-form__button">Создать</button>
  </form>
</template>
<script>
export default {
  name: 'TimerCreationForm',
  data() {
    return {
      hours: 0,
      minutes: 0,
      seconds: 0,
    }
  },
  props: {
    addNewTimer: Function
  }
}
</script>
<style scoped>
.timer-creation-form {
  width: 225px;
  height: 120px;
  background-color: #696969;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 5px 20px;
  box-sizing: border-box;
  justify-content: space-between;
}

.timer-creation-form__input {
  padding: 0;
  box-sizing: border-box;
  background-color: transparent;
  border: 1px solid #fff;
  color: #fff;
  width: 100%;
  text-align: center;
  outline: none;
}

.timer-creation-form__input::placeholder {
  color: #fff;
}

.timer-creation-form__button {
  width: 100%;
  box-sizing: border-box;
  background-color: transparent;
  color: #fff;
  border: 1px solid #fff;
  cursor: pointer;
  transition: all 0.2s ease-in-out;
}

.timer-creation-form__button:hover {
  transform: scale(1.1);
}
</style>