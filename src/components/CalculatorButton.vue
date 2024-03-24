<script setup lang="ts">
const props = defineProps({
  text: String,
  action: Function as unknown as unknown as unknown as () => void | string
});

</script>

<template>
  <a href="#" :onclick="props.action">
    <div :class="text != 'Clear' ? 'bg-sky-400 hover:bg-sky-500 w-14 transition-colors px-5 py-2 text-white text-xl font-bold grid place-items-center h-full rounded-lg' : 'bg-red-400 hover:bg-red-500 w-max transition-colors px-5 py-2 text-white text-xl font-bold grid place-items-center h-full rounded-lg'">
      {{ props.text }}
    </div>
  </a>
</template>