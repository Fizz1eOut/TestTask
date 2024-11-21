<script setup lang="ts">
import { ref } from 'vue';
import CallbackModal from '@/components/Content/CallbackModal.vue';

const active = ref(false);
</script>

<template>
  <div class="tree-modal">
    <button @click="active = true" class="button">
      Открыть
    </button>

    <callback-modal v-model="active" />
  </div>
</template>

<style scoped>
  .tree-modal {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100vh;
  }
  .button {
    font-size: 32px;
    color: var(--color-blue);
    cursor: pointer;
    background-color: transparent;
  }
</style>
