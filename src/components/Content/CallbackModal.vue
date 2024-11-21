<script setup lang="ts">
  import { ref, reactive, defineEmits } from 'vue';
  import AppModal from '@/components/Base/AppModal.vue';
  import FolderTree from '@/components/Content/FolderTree.vue';
  import ModalFooter from '@/components/Content/ModalFooter.vue';

  const emit = defineEmits(['update:modelValue', 'select']);

  interface Folder {
    id: number;
    name: string;
    children: Folder[];
    isOpen?: boolean;
  }

  const initializeFolders = (folders: Omit<Folder, 'isOpen'>[]): Folder[] => {
    return folders.map(folder => ({
      ...folder,
      isOpen: false,
      children: initializeFolders(folder.children || []),
    }));
  };

  const mockFoldersData: Omit<Folder, 'isOpen'>[] = [
    { id: 1, name: 'Папка 1', children: [
      { id: 2, name: 'Папка 1.1', children: [] },
      { id: 3, name: 'Папка 1.2', children: [
          { id: 4, name: 'Папка 1.2.1', children: [] },
      ]},
    ]},
    { id: 5, name: 'Папка 2', children: [] },
  ];

  const mockFolders = reactive<Folder[]>(initializeFolders(mockFoldersData));

  const selectedFolderName = ref<string | null>(null);

  const selectFolder = (folderName: string) => {
    selectedFolderName.value = folderName;  // Сохраняем только имя папки
  };

  const close = () => {
    emit('update:modelValue', false);
  };

  const confirmSelection = () => {
    if (selectedFolderName.value) {
      emit('select', selectedFolderName.value);  // Передаем имя папки
    }
    close();
  };
</script>

<template>
  <app-modal>
    <folder-tree
      :folders="mockFolders"
      :selected-folder-id="selectedFolderName"
      @select="selectFolder"
    />

    <modal-footer
      :selectedFolderId="selectedFolderName"
      @select="confirmSelection"
    />
    <button class="button-close" @click="close">Закрыть</button>
  </app-modal>
</template>

<style scoped>
  .button-close {
    margin-top: 10px;
    font-size: 18px;
    background-color: transparent;
  }
</style>
