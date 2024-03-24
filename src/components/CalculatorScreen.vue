<script setup lang="ts">
import { defineProps } from 'vue';

const props = defineProps({
  value: String
})
</script>

<template>
  <div class="bg-gray-400 rounded-md text-white font-bold text-3xl flex justify-end items-center px-4 py-2 w-[11.5rem] overflow-x-hidden">
    <span :class="{ 'blink': props.value === '' }">{{ props.value !== '' ? props.value : "_" }}</span>
  </div>
</template>

<style>
.blink {
  animation: blink-animation 1s step-end infinite;
}

@keyframes blink-animation {
  0% {
    opacity: 1;
  }
  50% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
</style>