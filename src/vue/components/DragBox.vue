<script setup lang="ts">

</script>

<template>
  <div @dragover.prevent.stop="onDragOverBox($event, 'first')">
    <transition-group name="dragItemList">
      <slot :name="" :items=""></slot>
    </transition-group>
  </div>
</template>

<style scoped>
.dragItemList {
  transition: 100;
}
</style>
