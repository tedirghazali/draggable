<script setup lang="ts">
import { ref } from 'vue'
import DragBox from './components/DragBox.vue'

const firstItems = ref([
  {id: 1, name: 'Option 1', order: 1},
  {id: 2, name: 'Option 2', order: 2},
  {id: 3, name: 'Option 3', order: 3},
  {id: 7, name: 'Option 7', order: 4},
  {id: 8, name: 'Option 8', order: 5},
  {id: 9, name: 'Option 9', order: 6},
  {id: 10, name: 'Option 10', order: 7},
  {id: 11, name: 'Option 11', order: 8},
  {id: 12, name: 'Option 12', order: 9},
])

const secondItems = ref([
  {id: 4, name: 'Option 4', order: 1},
  {id: 5, name: 'Option 5', order: 2},
  {id: 6, name: 'Option 6', order: 3},
])
</script>

<template>
  <div class="container mt-30px mb-30px">
    <div class="d-flex">
      <div class="w-50pct pr-10px">
        <DragBox class="list">
        
        </DragBox>
      </div>
      <div class="w-50pct pl-10px">
        <DragBox class="list">
        
        </DragBox>
      </div>
    </div>
  </div>
</template>

<style>
@use base;
@use container;
@use list;
</style>
