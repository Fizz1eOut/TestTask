<script setup lang="ts">
const props = defineProps({
  title: {
    type: String,
    required: true,
  },
});

const emit = defineEmits(['close']);
</script>

<template>
  <div class="modal-header">
    <h2 class="modal-header__title">
      {{ props.title }}
    </h2>

    <div class="modal-header__button">
      <button class="button-close" @click="emit('close')">
        Закрыть
      </button>
    </div>
  </div>
</template>

<style scoped>
  .modal-header {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    gap: 10px;
  }
  .modal-header__title {
    font-size: 20px;
  }
  .button-close {
    font-size: 20px;
    color: var(--color-black);
    background-color: transparent;
    cursor: pointer;
  }
</style>
