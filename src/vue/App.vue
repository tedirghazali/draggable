<script setup lang="ts">
import { ref, computed } from 'vue'
import DragBox from './components/DragBox.vue'
import DragItem from './components/DragItem.vue'

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

const firstStateItems = ref(firstItems.value.map((item: any, index: number) => {
  item['order'] = Number(index) + 1
  item['drag'] = false
  return item
}))

const secondStateItems = ref(secondItems.value.map((item: any, index: number) => {
  item['order'] = Number(index) + 1
  item['drag'] = false
  return item
}))

const firstMappedItems = computed(() => {
  return firstStateItems.value.sort((a: any, b:any) => Number(a.order) - Number(b.order))
})

const secondMappedItems = computed(() => {
  return secondStateItems.value.sort((a: any, b: any) => Number(a.order) - Number(b.order))
})

const onDrop = (order: number) => {
  console.log(order)
}

const itemId = ref('')

const onFirstDragStart = (uniqid: string | number, item: any) => {
  itemId.value = uniqid
}

const onFirstDragEnd = (order: number, uniqid: string | number, item: any) => {
  if(String(itemId.value) !== String(uniqid)) {
    //console.log('yes')
  }
  firstStateItems.value = firstStateItems.value.map((item: any) => {
    item.drag = false
    return item
  })
}

const onFirstDragOver = (order: number, item: any) => {
  firstStateItems.value = firstStateItems.value.map((i: any, ind: number) => {
    if(String(i.id) === String(itemId.value)) {
      i.order = order
      i.drag = true
    }
    return i
  }).sort((a: any, b: any) => Number(a.order) - Number(b.order)).map((item: any, index: number) => {
    item.order = Number(index) + 1
    return item
  })
}

const onSecondDragStart = (uniqid: string | number, item: any) => {
  itemId.value = uniqid
}

const onSecondDragEnd = (order: number, uniqid: string | number, item: any) => {
  if(String(itemId.value) !== String(uniqid)) {
    //console.log('yes')
  }
  secondStateItems.value = secondStateItems.value.map((item: any) => {
    item.drag = false
    return item
  })
}

const onSecondDrag = (order: number, item: any) => {
  secondStateItems.value = secondStateItems.value.map((i: any, ind: number) => {
    if(String(i.id) === String(itemId.value)) {
      i.order = order
      i.drag = true
    }
    return i
  }).sort((a: any, b: any) => Number(a.order) - Number(b.order)).map((item: any, index: number) => {
    item.order = Number(index) + 1
    return item
  })
}
</script>

<template>
  <div class="container mt-30px mb-30px">
    <div class="d-flex">
      <div class="w-50pct pr-10px">
        <DragBox class="list" @drop="onDrop">
          <transition-group name="dragItemList">
            <DragItem 
              class="listItem"
              v-for="(item, index) in firstMappedItems" :key="index"
              :order="item.order"
              :item="item"
              :uniqid="item.id"
              @over="onFirstDragOver"
              @start="onFirstDragStart"
              @end="onFirstDragEnd">{{ item.name }}</DragItem>
          </transition-group>
        </DragBox>
      </div>
      <div class="w-50pct pl-10px">
        <DragBox class="list" @drop="onDrop">
          <transition-group name="dragItemList">
            <DragItem 
              class="listItem"
              v-for="(item, index) in secondMappedItems" :key="index"
              :order="item.order"
              :item="item"
              :uniqid="item.id"
              @over="onSecondDrag"
              @start="onSecondDragStart"
              @end="onSecondDragEnd">{{ item.name }}</DragItem>
          </transition-group>
        </DragBox>
      </div>
    </div>
  </div>
</template>

<style>
@use base;
@use container;
@use list;

.dragItemList {
  transition: 100;
}
</style>
