<script setup>
const props = defineProps(['isInfoPopapVisible']);
const emit = defineEmits(['closePopap']);

const closePopap = () => {
  emit('closePopap');
};

closePopap();
</script>

<template>
  <div v-show="isInfoPopapVisible" class="p-4 bg-white">
    <div
      class="max-w-screen-xl w-4/5 max-h-full fixed top-50 left-0 right-0 z-10 mx-auto p-8 bg-white"
      style="height: calc(100% - 3.5rem); box-shadow: 15px 15px 0px 0px #f9eba7;"
    >
      <div class="w-full flex justify-between items-center">
        <div>
        </div>

        <button @click="closePopap">
          <span class="flex uppercase gap-2"
            >Calendar
            <i class="material-icons">arrow_forward</i>
          </span>
        </button>
      </div>

      <div class="flex justify-center items-center">
        <slot></slot>
      </div>
    </div>
    <div
      class="fixed top-0 left-0 right-0 z-0 max-w-595 w-full mx-auto h-full bg-gray-700 bg-opacity-60"
      id="popapBg"
    ></div>
  </div>
</template>

<style scoped></style>
