<script setup lang="ts">
import { ref } from 'vue';
import HeaderMsg from './components/HeaderMsg.vue'
import Content from './components/Content.vue'

const headerTitle = ref('反恐精英: 全球攻势 可视化数据')
const contentTotal = ref('最高在线人数')
const contentCurrent = ref('平均在线人数')

</script>

<template>
  <HeaderMsg :title="headerTitle" />
  <Content 
    :totalText="contentTotal" 
    :currentText="contentCurrent" 
  />
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  list-style: none;
  text-decoration: none;
  box-sizing: border-box;
  font-size: 16px;
}
html {
  height: 100%;
}
body {
  height: inherit;
  background: url('./assets/bg.jpg') no-repeat top center;
}
#app {
  min-width: 1024px;
  height: inherit;
  display: flex;
  flex-direction: column;
  overflow-y: scroll;
  &::-webkit-scrollbar {
    width: 6px;
  }
  &::-webkit-scrollbar-thumb {
    background-color: #a5a5a51a;
  }
}
</style>
