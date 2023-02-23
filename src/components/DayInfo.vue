<script setup>
const props = defineProps(['day', 'text']);
</script>

<template>
  <div class="my-6 flex justify-center items-center flex-col">
    <div class="mb-6 text-xl md:text-4xl font-bold">{{ day }}</div>
    <div class="w-3/4 text-xl md:text-4xl font-bold text-gray-300 text-left">"{{ text }}"</div>
  </div>
</template>
