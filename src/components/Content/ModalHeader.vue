<script setup lang="ts">
import { defineProps } from 'vue';
const props = defineProps({
  title: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <div class="modal-header">
    <h2 class="modal-header__title">
      {{ props.title }}
    </h2>
  </div>
</template>

<style scoped>
  .modal-header__title {
    font-size: 20px;
  }
</style>
