<script setup lang="ts">
const props = defineProps({
  selectedFolderId: {
    type: [String, null],
    default: null,
  },
});

const emit = defineEmits(['select']);

const confirmSelection = () => {
  if (props.selectedFolderId !== null) {
    emit('select', props.selectedFolderId);
  }
};
</script>

<template>
  <div class="modal-footer">
    <button 
      @click="confirmSelection"
      :disabled="!selectedFolderId"
      class="modal-footer__button button"
    >
      Ок
    </button>
  </div>
</template>

<style scoped>
  .modal-footer__button {
    font-size: 18px;
    background-color: transparent;
  }
</style>
