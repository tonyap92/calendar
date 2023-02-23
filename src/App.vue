<script setup>
import { RouterView } from 'vue-router';
</script>

<template>
  <div
    class="max-w-screen-xl w-full my-0 mx-auto py-16 px-3 xs:px-24 xs:py-24 font-sans text-black bg-white box-border overflow-hidden"
  >
    <RouterView v-slot="{ Component }">
      <keep-alive>
        <component :is="Component" />
      </keep-alive>
    </RouterView>
  </div>
</template>

<style scoped></style>
