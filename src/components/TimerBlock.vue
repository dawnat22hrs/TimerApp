<script setup>
import { ref } from "vue";
import PauseIcon from "./icons/PauseIcon.vue"

//state
const start = ref(true)
const delimiterSeconds = ref(false)
const delimiterMinutes = ref(false)
let isActive = ""
let hours = ref(''),
    minutes = ref(''),
    seconds = ref('0'),
    interval;

//methods
const startTimerBtn = () => {
    clearInterval(interval)
    interval = setInterval(startTimer, 1000)
    start.value = false
    getActive(start.value)
}

const pauseTimerBtn = () => {
    start.value = true
    clearInterval(interval)
    getActive(start.value)
}

const startTimer = () => {
    seconds.value++
    if (seconds.value  > 59){
        minutes.value++
        delimiterSeconds.value = true
        seconds.value = 0 
    }

    if (minutes.value > 59){
        hours.value++
        delimiterMinutes.value = true
        minutes.value = 0
    }
}

const getActive = (start) => {
    if ( start == false ) {
        isActive = "#fff"
    }
    if (start == true){
        isActive = "#9E9E9E"
    }
}

defineEmits(['onResetTimer'])
</script>

<template>
    <div class="timer-block">
        <div class="timer-block__time-value" :style="{color: isActive, borderBottomColor: isActive}">
            <div class="timer hours">{{ hours }}</div>
            <div v-if="delimiterMinutes" class="timer">:</div>
            <div class="timer minutes">{{ minutes }}</div>
            <div v-if="delimiterSeconds" class="timer">:</div>
            <div class="timer seconds">{{ seconds }}</div>
        </div>
        <div class="timer-block__time-control">
            <div class="start-pause-btn">
                <div class="start-btn" v-if="start" @click="startTimerBtn"></div>
                <div class="pause-btn" v-else @click="pauseTimerBtn"><PauseIcon :style="{background: '#696969', fill: isActive}"/></div>
                <!--Не понял "Сброс" должен обнулять таймер или удалять сам блок. Сделал сброс как удаление блока-->
                <div class="reset-btn" @click="$emit('onResetTimer')" :style="{background: isActive}"></div>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
.timer-block {
    width: 225px;
    height: 120px;
    background: #696969;
    display: flex;
    flex-direction: column;

    &__time-value {
        border-bottom: 1px solid #9E9E9E;
        color: #9E9E9E;
        background: none;
        height: 60px;
        display: flex;
        align-items: center;
        justify-content: center;

        .timer {
            background: none;
            font-style: normal;
            font-weight: 400;
            font-size: 22px;
            line-height: 21px;
        }
    }

    &__time-control {

        display: flex;
        height: 60px;
        background: none;
        justify-content: center;
        align-items: center;

        .start-pause-btn {
            background: #696969;
            display: flex;
            width: 85px;
            justify-content: space-between;

            .start-btn {
                background: #696969;
                width: 0;
                height: 0;
                border-left: 10px solid transparent;
                border-right: 10px solid transparent;
                border-bottom: 17px solid #9E9E9E;
                rotate: 90deg;
            }

            .pause-btn {
                background: #696969;
            }

            .reset-btn{
                background: #9E9E9E;
                width: 20px;
                height: 20px;
                position: relative;
            }
        }
    }
}
</style>