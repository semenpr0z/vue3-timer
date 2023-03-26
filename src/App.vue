<script>
import Timer from '@/components/Timer.vue';

export default {
  data() {
    return {
      counter: 1,
      timers: [
        { id: 1 }
      ]
    }
  },
  components: {
    Timer
  },
  methods: {
    addNewTimer() {
      this.counter++
      this.timers.push({ id: this.counter })
    }
  }
}
</script>

<template>
  <main>
    <TransitionGroup name="timers">
      <Timer v-for="timer in timers" :key="timer.id" />
    </TransitionGroup>
    <button class="add-new-timer" @click="addNewTimer" key="btn"></button>
  </main>
</template>

<style lang='scss'>
@import '@/assets/styles/global.scss';

main {
  padding: 72px 0px;
  margin: 0 auto;
  display: grid;
  grid-row-gap: 45px;
  grid-column-gap: 50px;
  max-width: fit-content;
}

.add-new-timer {
  width: 225px;
  height: 120px;
  background-image: url('/img/add-timer.png');
  padding: 0;
  border: none;
  cursor: pointer;
}

@media (min-width: 1024px) {
  main {
    grid-template-columns: repeat(3, 225px);
    max-width: 775px;
  }
}

@media (min-width: 768px) and (max-width: 1023px) {
  main {
    grid-template-columns: repeat(2, 225px);
    max-width: 500px;
  }
}

@media (min-width: 320px) and (max-width: 767px) {
  main {
    grid-template-columns: repeat(1, 225px);
    max-width: 225px;
  }
}

.timers-enter-active,
.timers-leave-active {
  transition: opacity 1s;
}

.timers-enter-from,
.timers-leave-to {
  opacity: 0;
}
</style>