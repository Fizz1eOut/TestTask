<script setup lang="ts">
interface Folder {
  id: number;
  name: string;
  children: Folder[];
  isOpen?: boolean;
}

const props = defineProps({
  folders: {
    type: Array as () => Folder[],
    required: true,
  },
  selectedFolderId: {
    type: [String, null],
    default: null,
  },
});

const emit = defineEmits(['select']);

const toggleOpen = (folder: Folder) => {
  folder.isOpen = !folder.isOpen;
};

const selectFolder = (folder: Folder) => {
  emit('select', folder.name);  // Передаем только имя папки
};
</script>

<template>
  <ul class="folder-tree">
    <li v-for="folder in props.folders" :key="folder.id">
      <div class="folder-node">
        <button @click="toggleOpen(folder)">
          {{ folder.isOpen ? '-' : '+' }}
        </button>
        <span
          :class="{ selected: folder.name === selectedFolderId }"
          @click="selectFolder(folder)"
        >
          {{ folder.name }}
        </span>
      </div>
      <folder-tree
        v-if="folder.isOpen && folder.children.length"
        :folders="folder.children"
        :selected-folder-id="selectedFolderId"
        @select="emit('select', $event)"
      />
    </li>
  </ul>
</template>

<style scoped>
.folder-node {
  display: flex;
  align-items: center;
  margin: 5px 0;
}

.folder-node button {
  margin-right: 5px;
  font-size: 20px;
  background-color: transparent;
}

.selected {
  font-weight: bold;
  color: blue;
}
</style>
