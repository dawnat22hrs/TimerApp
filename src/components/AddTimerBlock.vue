<script setup>
import AddIcon from './icons/AddIcon.vue';

defineEmits(['addTimer'])
</script>

<template>
    <div class="add-block" @click="$emit('addTimer')">
        <AddIcon style="background: #696969;"/>
    </div>
</template>

<style scoped lang="scss">
.add-block {
    width: 225px;
    height: 120px;
    background: #696969;
    display: flex;
    align-items: center;
    justify-content: center;
}
</style>