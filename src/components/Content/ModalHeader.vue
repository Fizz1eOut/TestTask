<script setup lang="ts">
const emit = defineEmits(['close']);
</script>

<template>
  <button class="button-close" @click="emit('close')">
    Закрыть
  </button>
</template>

<style scoped>
.button-close {
  font-size: 20px;
  color: var(--color-black);
  background-color: transparent;
  cursor: pointer;
}
</style>
