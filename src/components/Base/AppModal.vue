<script setup lang="ts">
import {  defineEmits } from 'vue';
import ModalHeader from '@/components/Content/ModalHeader.vue';

const props = defineProps({
  modelValue: {
    type: Boolean,
    required: false,
    default: false,
  },
});

const emit = defineEmits(['update:modelValue']);

const close = () => {
  emit('update:modelValue', false);
};
</script>

<template>
  <Teleport to="body">
    <Transition>
      <div v-if="props.modelValue" class="modal">
        <div class="overlay" @click.self="close">
          <div class="content">
              <modal-header :title="'Мой заголовок'" @close="close" />
              <div class="content__body">
                <slot />
              </div>
          </div>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<style scoped>
  .content__body {
    padding: 20px 0;
  }
  .overlay {
    position: fixed;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    z-index: 11;
    background-color: rgba(0, 0, 0, 0.7);
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    width: 100%;
  }
  .content {
    border-radius: 10px;
    background: #eef5fc;
    max-width: 300px;
    width: 100%;
    padding: 20px;
  }
  .title {
    color: var(--color-black);
    font-size: 26px;
    font-style: normal;
    font-weight: 400;
    line-height: 140%;
  }
  .title span {
    font-size: 26px;
    font-style: normal;
    font-weight: 600;
    line-height: 140%;
  }
  @media (max-width: 499px) {
    .content {
      padding: 20px 20px 40px;
    }
  }
  .v-enter-active,
  .v-leave-active {
    transition: opacity 0.5s ease;
  }

  .v-enter-from,
  .v-leave-to {
    opacity: 0;
  }
</style>
