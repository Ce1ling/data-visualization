<script setup lang="ts">
import { reactive } from 'vue'
import MiniChart from './MiniChart.vue';

const leftList = reactive([
  { title: 'L 1' },
  { title: 'L 2' },
  { title: 'L 3' },
])
const rightList = reactive([
  { title: 'R 1' },
  { title: 'R 2' },
  { title: 'R 3' },
])

</script>

<template>
  <main class="content">
    <section class="content-left">
      <MiniChart :list="leftList" />
    </section>
    <section class="content-middle">
      <div class="middle-header">
        header
      </div>
      <div class="middle-body">
        body
      </div>
    </section>
    <section class="content-right">
      <MiniChart :list="rightList" />
    </section>
  </main>
</template>

<style scoped lang="scss">
.content {
  color: #fff;
  display: flex;
  padding: 20px;
  height: 100%;
  gap: 10px;
  &-left,
  &-right {
    flex: 3;
  }
  &-middle {
    flex: 5;
    display: flex;
    flex-direction: column;
    gap: 10px;
    .middle-header {
      padding: 10px;
      background-color: #ffffff20;
    }
    .middle-body {
      height: 100%;
      padding: 10px;
      background-color: #ffffff20;
    }
  }
}
</style>