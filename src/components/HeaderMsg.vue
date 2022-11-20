<script setup lang="ts">
import { ref, onMounted, onUnmounted, computed } from 'vue';

interface Props {
  title?: string
  showDate?: boolean
}
const props = withDefaults(defineProps<Props>(), {
  title: '数据可视化',
  showDate: true
})


// 获取当前日期、时间
const getCurrentDate = () => {
  const dt = new Date()
  const y = dt.getFullYear()
  const m = (dt.getMonth() + 1).toString().padStart(2, '0')
  const d = dt.getDate().toString().padStart(2, '0')
  return `${y}年${m}月${d}日`
}
const getCurrentTime = () => {
  const dt = new Date()
  const hh = dt.getHours().toString().padStart(2, '0')
  const mm = dt.getMinutes().toString().padStart(2, '0')
  const ss = dt.getSeconds().toString().padStart(2, '0')
  return `${hh}时${mm}分${ss}秒` 
}
const currentDate = ref(getCurrentDate())
const currentTime = ref(getCurrentTime())
const timeSection = computed(() => {
  /* 
    凌晨:3:00--6:00
    早晨:6:00---8:00
    上午:8:00--11:00
    中午:11:00--13:00
    下午:13:00--17:00
    傍晚:17:00--19:00
    晚上:19:00--23:00
    深夜:23:00--3:00
  */
  const dt = new Date();
  const hh = dt.getHours();
  if (hh >= 3 && hh <= 6) {
    return '凌晨'
  } else if (hh >= 6 && hh <= 8) {
    return '早晨'
  } else if (hh >= 8 && hh <= 11) {
    return '上午'
  } else if (hh >= 11 && hh <= 13) {
    return '中午'
  } else if (hh >= 13 && hh <= 17) {
    return '下午'
  } else if (hh >= 17 && hh <= 19) {
    return '傍晚'
  } else if (hh >= 19 && hh <= 23) {
    return '晚上'
  } else {
    return '深夜'
  }
})


let timer = ref(0);
onMounted(() => {
  timer.value = setInterval(() => {
    currentDate.value = getCurrentDate()
    currentTime.value = getCurrentTime()
  }, 1000)
})
onUnmounted(() => {
  clearInterval(timer.value)
})

</script>

<template>
  <header class="header">
    <h1 class="title">
      {{ props.title }}
    </h1>
    <div class="date-time" v-if="showDate">
      现在是 {{ currentDate }}
      {{ timeSection }} {{ currentTime }}
    </div>
  </header>
</template>

<style scoped lang="scss">
.header {
  background: url('../assets/header-bg.png') top center;
  height: 80px;
  color: #fff;
  position: relative;
  .title {
    font-size: 22px;
    text-align: center;
    line-height: 80px;
  }
  .date-time {
    position: absolute;
    top: 0;
    right: 20px;
    line-height: 80px;
    color: gray;
    font-size: 14px;
  }
}
</style>