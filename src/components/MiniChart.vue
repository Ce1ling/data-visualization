<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue'
import * as echarts from 'echarts'

interface Props {
  title?: string
  dynamicData?: number[]
  option: unknown
}
const props = defineProps<Props>()

type Chart = {
  setOption: (options: echarts.EChartsOption) => void
}
const dynamicChartRun = (list: number[], chart: Chart) => {
  list.forEach((_, i) => {
    if (Math.random() > 0.9) {
      list[i] += Math.round(Math.random() * 60000)
    } else {
      list[i] += Math.round(Math.random() * 6000)
    }
  })
  chart.setOption({
    series: {
      type: 'bar',
      data: list
    }
  })
}

const chart = ref()
let dynamicTimer = ref(0)
onMounted(() => {
  // 初始化 chart 并设置数据
  const c = echarts.init(chart.value)
  c.setOption(props.option as echarts.EChartsOption)
  window.addEventListener('resize', () => {
    c.resize()
  })

  // 如果是动态 chart
  if (props.dynamicData) {
    const list = props.dynamicData
    setTimeout(() => dynamicChartRun(list, c), 0)
    dynamicTimer.value = setInterval(() => dynamicChartRun(list, c), 3000)
  }
})
onUnmounted(() => {
  clearInterval(dynamicTimer.value)
})

</script>

<template>
  <div class="mini-chart">
    <h2>{{ props.title }}</h2>
    <div class="mini-chart-chart" ref="chart"></div>
    <div class="mini-chart-footer"></div>
  </div>
</template>

<style scoped lang="scss">
.mini-chart {
  flex: 1;
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
    width: 100%;
    height: 100%;
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