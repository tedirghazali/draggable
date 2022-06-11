<script setup lang="ts">
const emit = defineEmits<{
  (e: 'drop', order: any): void
}>()

const onDragOverBox = (dragId: number, event: any) => {
  emit('drop', dragId)
}
</script>

<template>
  <div @dragover.prevent.stop="onDragOverBox(0, $event)">
    <slot></slot>
  </div>
</template>
