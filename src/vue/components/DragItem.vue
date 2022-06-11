<script setup lang="ts">
import { ref } from 'vue'

const props = defineProps<{
  order: number,
  item: any,
  uniqid: string | number
}>()

const emit = defineEmits<{
  (e: 'over', order: number, item: any): void
  (e: 'start', uniqid: string | number, item: any): void
  (e: 'end', order: number, uniqid: string | number, item: any): void
}>()

const dragItem = ref(props.item || {})
const dragElem = ref(null)

const onTransitionStart = () => {
  
}

const onTransitionEnd = () => {

}

const onDragOverItem = (dragId: number) => {
  emit('over', dragId, dragItem.value)
}

const onDragStartItem = () => {
  emit('start', props.uniqid, dragItem.value)
}

const onDragEndItem = (dragId: number) => {
  emit('end', dragId, props.uniqid, dragItem.value)
}
</script>

<template>
  <div 
    draggable="true" 
    @transitionStart="onTransitionStart"
    @transitionEnd="onTransitionEnd"
    @dragover.prevent.stop="onDragOverItem(order)"
    @dragstart.stop="onDragStartItem"
    @dragend.stop="onDragEndItem(order)"
    @dragenter.prevent
    ref="dragElem"
    :class="{ active: item.drag }">
    <slot></slot>
  </div>
</template>

<style scoped>
.isDragging {
  opacity: 0.4;
}
</style>
