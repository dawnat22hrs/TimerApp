<script setup>
import { ref } from 'vue';
import vAutoAnimate from '@formkit/auto-animate'
import TimerList from '../components/TimerList.vue'

const timers = ref([])

const addTimer = () => timers.value.push({id: timers.value.length - 1})

const resetTimer = (id) => timers.value = timers.value.filter(x => x.id !== id)
</script>

<template>
  <main>
    <TimerList
      v-auto-animate 
      @on-reset="resetTimer"
      @add-timer="addTimer"
      :timers="timers"
    />
  </main>
</template>