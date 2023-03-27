<script setup>
import TimerBlock from './TimerBlock.vue';
import AddTimerBlock from './AddTimerBlock.vue';

const emits = defineEmits(['addTimer'])
defineProps({
    timers: Array,
})

const addTimer = () => emits('addTimer')
const onResetTimer = (id) => emits('onReset', id)
</script>

<template>
  <div class="timer-list">
    <TimerBlock 
        v-for="timer in timers" 
        :key="timer.id"
        @on-reset-timer="onResetTimer(timer.id)"
    />
    <AddTimerBlock @add-timer="addTimer"/>
  </div>
</template>

<style scoped lang="scss">
.timer-list {
    width: 776px;
    margin: 72px auto 82px;

    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-column-gap: 50px;
    grid-row-gap: 45px;
}

@media screen and (min-width: 768px) and (max-width: 1023px){
  .timer-list {
    width: 500px;
    margin: 72px auto;

    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-column-gap: 50px;
    grid-row-gap: 45px;
  }
}

@media screen and (min-width: 320px) and (max-width: 767px){
  .timer-list {
    width: 225px;
    margin: 72px auto 77px;

    display: grid;
    grid-template-columns: repeat(1, 1fr);
    grid-row-gap: 45px;
  }
}
</style>
