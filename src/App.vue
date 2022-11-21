<script setup lang="ts">
import HeaderMsg from './components/HeaderMsg.vue'
import Content from './components/Content.vue'

</script>

<template>
  <HeaderMsg />
  <Content />
</template>

<style>
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
  overflow: hidden;
}
</style>
