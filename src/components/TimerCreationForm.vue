<template>
  <form class="timer-creation-form" @submit.prevent="() => addNewTimer(this.hours, this.minutes, this.seconds)">
    <label class="timer-creation-form__label">
      Часы
      <input
        @input="hours = $event.target.value"
        class="timer-creation-form__input"
        v-bind:value="hours"
        placeholder="Часы"
        type="number"
        v-bind:min="0"
        v-bind:max="999"
      />
    </label>
    <label class="timer-creation-form__label">
      Минуты
      <input
        @input="minutes = $event.target.value"
        class="timer-creation-form__input"
        v-bind:value="minutes"
        placeholder="Минуты"
        type="number"
        v-bind:min="0"
        v-bind:max="60"
      />
    </label>
    <label class="timer-creation-form__label">
      Секунды
    <input
      @input="seconds = $event.target.value"
      class="timer-creation-form__input"
      v-bind:value="seconds"
      placeholder="Секунды"
      type="number"
      v-bind:min="0"
      v-bind:max="60"
    />
    </label>
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
  text-align: center;
  outline: none;
  width: 100px;
}

.timer-creation-form__input::placeholder {
  color: #9e9e9e;
  text-align: start;
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

.timer-creation-form__label {
  display: flex;
  justify-content: space-between;
  width: 100%;
}
</style>