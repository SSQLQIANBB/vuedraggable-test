<template>
<div class="container">
  <div class="left">
    <draggable
      class="wrapper"
      :group="{name: 'form', pull: 'clone', put: false}"
      :ghost-class="ghost"
      :list="list"
      :sort="false"
      itemKey="id"
      :clone="clone"
    >
      <template #item="{ element: field }">
        <li>{{ field.name }}</li>
      </template>
    </draggable>
  </div>
  <div class="right">
    <draggable
      class="form-wrapper"
      :group="{name: 'form'}"
      ghost-class="ghost"
      fallback-class="fallback"
      :list="widgetlist"
      :animation="300"
      @add="handleAdd"
    >
      <template #item="{ element: field }">
        <draggable
          class="form-row-wrapper"
          :group="{name: 'form'}"
          ghost-class="ghost"
          fallback-class="fallback"
          :list="field"
          :animation="300"
          @add="e => handleAddItem(e, field)"
          @start="onStart"
          :style="{display: 'grid', gridTemplateColumns: `repeat(${field.length}, 1fr)`}"
        >
        <template #item="{ element: item }">
           <li>{{ item.name }}</li>
        </template>
        </draggable>
      </template>
    </draggable>
  </div>
</div>
</template>

<script lang="ts" setup>
import Draggable from 'vuedraggable';
import { ref } from 'vue';

const list = [
  {
    id: 1,
    name: '输入框'
  },
  {
    id: 2,
    name: '选择框',
  }
]

const widgetlist = ref([])

function clone(origin: any, aaa) {
  console.log(aaa)
  return [origin]; 
}

function handleAdd() {
  console.log('widgetlist---handleAdd', widgetlist.value)
}

function handleAddItem(e, field) {
  const index = e.newIndex;
  // if (e.to.name === 'form-row-wrapper') {
  //   field.splice()
  // }

  console.log('------item-add-----')
  Array.isArray(field[index]) && field.splice(index, 1, field[index][0])

  console.log('item', e.draggedContext);
  console.log('item---to', e.to.className);

  console.log('widgetlist', widgetlist.value)
}

function onStart(e) {
  console.log('onstart', e)
}

</script>

<style lang="less" scoped>
.container {
  width: 100%;
  height: 100%;
  display: flex;
}
  .left {
    width: 300px;
    height: 100%;
    background: #eee;
    padding: 12px;
    li {
      display: inline-block;
      min-width: 35%;
      padding: 6px 12px;
      background: skyblue;
      border-radius: 6px;
      list-style: none;
      margin-bottom: 12px;
      margin-left: 12px;
    }
  }
  .right {
    flex: 1;
    height: 100%;
    .form-wrapper {
      width: 100%;
      height: 100%;
      list-style: none;
      li {
        padding: 20px 12px;
        background: #ccc;
        margin-bottom: 12px;
        border-radius: 6px;
      }
      :deep(.ghost) {
        border-top: 3px solid #3086f3;
      }
    }
  }

</style>
