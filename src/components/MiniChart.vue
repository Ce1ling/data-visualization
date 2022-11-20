<script setup lang="ts">
const props = defineProps<{
  list?: Array<{ title: string }>
}>()


</script>

<template>
  <ul class="mini-chart-list">
    <li class="mini-chart-item" 
      v-for="(item, i) in props.list" 
      :key="i">
      <h2>{{ item.title }}</h2>
      <div class="mini-chart-item-chart"></div>
      <div class="mini-chart-item-footer"></div>
    </li>
  </ul>
</template>

<style scoped lang="scss">
.mini-chart-list {
  height: 100%;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.mini-chart-item {
  height: 100%;
  background-color: #ffffff20;
  position: relative;
  padding: 10px;
  &::before,
  &::after {
    content: '';
    position: absolute;
    width: 10px;
    height: 10px;
    border: 2px solid blueviolet;
  }
  &::before {
    top: 0;
    left: 0;
    border-right: transparent;
    border-bottom: transparent;
  }
  &::after {
    top: 0;
    right: 0;
    border-bottom: transparent;
    border-left: transparent;
  }
  h2 {
    text-align: center;
  }
  &-chart {
    // max-height: 220px;
    border: 1px solid red;
  }
  &-footer {
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 12px;
    &::before,
    &::after {
      content: '';
      position: absolute;
      width: 10px;
      height: 10px;
      border: 2px solid blueviolet;
    }
    &::before {
      top: 0;
      left: 0;
      border-top: transparent;
      border-right: transparent;
    }
    &::after {
      top: 0;
      right: 0;
      border-top: transparent;
      border-left: transparent;
    }
  }
}
</style>