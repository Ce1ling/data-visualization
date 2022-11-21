<script setup lang="ts">
import { ref, reactive } from 'vue'
import MiniChart from './MiniChart.vue';

interface Props {
  totalText?: string
  currentText?: string
}
const props = withDefaults(defineProps<Props>(), {
  totalText: '总量',
  currentText: '当前量'
})

const maxNumber = ref(1308963)
const avgNumber = ref(674665)


const getDynamicChartData = (len: number) => {
  const arr: number[] = []
  for (let i = 0; i < len; ++i) {
    arr.push(Math.round(Math.random() * (avgNumber.value / 2)));
  }
  return arr
}

const dynamicData = reactive(getDynamicChartData(3));
const leftList = reactive([
  { 
    title: '现役地图出场率', 
    option: {
      color: ['blueviolet'],
      tooltip: {
        trigger: 'item'
      },
      grid: {
        top: '5%',
        right: '5%',
        bottom: '15%',
        left: '10%'
      },
      xAxis: {
        type: 'category',
        data: ['Nuke', 'Mirage', 'Inferno', 'Ancient', 'Vertigo', 'Dust2', 'Overpass'],
        axisLabel: {
          color: '#fff',
          interval: 0
        }
      },
      yAxis: {
        type: 'value',
        axisLabel: {
          color: '#ffffff',
          formatter: '{value}%'
        },
        splitLine: {
          lineStyle: {
            color: '#ffffff5a'
          }
        }
      },
      series: [
        {
          data: [86, 70, 60, 55, 51, 40, 45],
          type: 'bar',
          barWidth: '50%'
        }
      ]
    }
  },
  { 
    title: '武器使用率(前五)', 
    option: {
      title: {
        left: 'center',
        textStyle: {
          color: '#fff'
        }
      },
      tooltip: {
        trigger: 'item'
      },
      legend: {
        orient: 'vertical',
        left: 'left',
        top: 'middle',
        textStyle: {
          color: 'inherit'
        }
      },
      series: [
        {
          type: 'pie',
          radius: '50%',
          data: [
            { value: 31.3, name: 'AK-47' },
            { value: 23.2, name: 'AWP' },
            { value: 20.8, name: 'M4A1-S' },
            { value: 16.5, name: 'Deagle' },
            { value: 8.6, name: 'USP' }
          ],
          // 鼠标移入时阴影
          emphasis: {
            itemStyle: {
              shadowBlur: 10,
              shadowOffsetX: 0,
              shadowColor: 'rgba(0, 0, 0, 0.5)'
            },
          },
        }
      ]
    }
  },
  { 
    title: '当前正在游戏人数',
    option: {
      tooltip: {
        trigger: 'axis'
      },
      grid: {
        top: '5%',
        right: '16%',
        bottom: '15%',
        left: '18%'
      },
      xAxis: {
        max: 'dataMax',
        axisLabel: {
          color: '#fff',
        }
      },
      yAxis: {
        type: 'category',
        data: ['优先竞技', '非优先竞技', '休闲模式'],
        axisLabel: {
          color: '#fff'
        },
        axisTick: {
          show: false
        },
        inverse: true,
        animationDuration: 300,
        animationDurationUpdate: 300,
        max: 2 // only the largest 3 bars will be displayed
      },
      series: {
        realtimeSort: true,
        type: 'bar',
        data: dynamicData,
        barWidth: '50%',
        label: {
          show: true,
          position: 'right',
          valueAnimation: true,
        },
        itemStyle: {
          barBorderRadius: 5
        }
      },
      animationDuration: 0,
      animationDurationUpdate: 3000,
      animationEasing: 'linear',
      animationEasingUpdate: 'linear'
    },
    dynamicData
  },
])
const rightList = reactive([
  { 
    title: '官方匹配玩家平均段位', 
    option: {
      tooltip: {
        show: true,
        confine: false,
      },
      legend: {
      },
      grid: {
        top: '5%',
        right: '5%',
        bottom: '15%',
        left: '14%',
      },
      xAxis: {
        type: 'value',
        axisLine: {
          show: true
        },
        axisLabel: {
          color: '#fff',
          formatter: '{value}%',
        },
        splitLine: {
          lineStyle: {
            color: '#ffffff5a',
          },
        },
      },
      yAxis: [
        {
          type: 'category',
          data: ['白银级', '黄金级', 'AK级', '菊花', '小老鹰', '大老鹰', '小地球', '大地球'],
          inverse: true,
          aixsLine: {
            show: false
          },
          axisTick: {
            show: false
          },
          axisLabel: {
            color: '#fff',
          },
        },
      ],
      series: [
        {
          type: 'bar',
          data: [29.3, 33.8, 21, 4.9, 3.8, 3.8, 2.6, 1],
          label: {
            show: true,
            formatter: '{c}%',
            color: '#fff',  
          },
          itemStyle: {
            color: (params: { dataIndex: number }) => {
              const colorList = ['#808080', '#d9cb36', '#367ed9', '#643e3e', '#001aff', '#7635a0', '#ff00e2', '#fa2f2f']
              return colorList[params.dataIndex]
            }
          }
        },
      ],
    }
  },
  { 
    title: 'CT 与 T 道具使用率', 
    option: {
      color: ['#67F9D8', '#FFE434', '#56A3F1', '#FF917C'],
      legend: {
        left: 'left',
        textStyle: {
          color: '#fff'
        }
      },
      radar: [
        {
          indicator: [
            { text: '烟雾弹' },
            { text: '闪光弹' },
            { text: '燃烧弹/瓶' },
            { text: '手榴弹' },
            { text: '诱饵弹' }
          ],
          radius: 50,
          startAngle: 90,
          splitNumber: 4,
          shape: 'circle',
          axisName: {
            formatter: '【{value}】',
            color: '#428BD4'
          },
          splitArea: {
            areaStyle: {
              color: ['#77EADF', '#26C3BE', '#64AFE9', '#428BD4'],
              shadowColor: 'rgba(0, 0, 0, 0.2)',
              shadowBlur: 10
            }
          },
          axisLine: {
            lineStyle: {
              color: 'rgba(211, 253, 250, 0.8)'
            }
          },
          splitLine: {
            lineStyle: {
              color: 'rgba(211, 253, 250, 0.8)'
            }
          }
        }
      ],
      series: [
        {
          type: 'radar',
          data: [
            {
              name: 'CT',
              value: [10, 6, 8, 5, 3],
            },
            {
              name: 'T',
              value: [8, 10, 9, 7, 2],
              areaStyle: {
                color: 'rgba(255, 228, 52, 0.6)'
              }
            }
          ],
          emphasis: {
            lineStyle: {
              width: 4
            }
          },
        }
      ]
    }
  },
  { 
    title: '玩家在线时段', 
    option: {
      tooltip: {
        trigger: 'item'
      },
      grid: {
        top: '5%',
        right: '5%',
        bottom: '15%',
        left: '15%'
      },
      xAxis: {
        type: 'category',
        data: ['00:00-08:00', '05:00-08:00', '08:00-11:00', '11:00-13:00', '13:00-16:00', '16:00-18:00', '18:00-23:00'],
        axisLabel: {
          color: '#fff'
        }
      },
      yAxis: {
        type: 'value',
        axisLabel: {
          color: '#fff'
        }
      },
      series: {
        type: 'line',
        data: [227813, 347561, 486872, 302137, 601734, 583146, 621235],
        max: 10,
        smooth: true,
        color: 'blueviolet'
      }
    }
  },
])

</script>

<template>
  <main class="content">
    <section class="content-left">
      <MiniChart 
        v-for="(item, i) in leftList" 
        :key="i" 
        :title="item.title" 
        :option="item.option"
        :dynamic-data="item.dynamicData"
      />
    </section>
    <section class="content-middle">
      <div class="middle-header">
        <div class="title">
          <p>{{ maxNumber }}</p>
          <p>{{ avgNumber }}</p>
        </div>
        <div class="desc">
          <p>{{ props.totalText }}</p>
          <p>{{ props.currentText }}</p>
        </div>
      </div>
      <div class="middle-body">
        <div class="global"></div>
        <div class="stars"></div>
        <div class="line"></div>
        <div class="map-chart"></div>
      </div>
    </section>
    <section class="content-right">
      <MiniChart 
        v-for="(item, i) in rightList" 
        :key="i" 
        :title="item.title" 
        :option="item.option"
      />
    </section>
  </main>
</template>

<style scoped lang="scss">
@keyframes rotate360 {
  from {
    transform: translate(-50%, -50%) rotate(0deg);
  }
  to {
    transform: translate(-50%, -50%) rotate(360deg);
  }
}

.content {
  color: #ffffff;
  display: flex;
  padding: 10px;
  height: 100%;
  gap: 10px;
  &-left,
  &-right {
    flex: 3;
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
  &-middle {
    flex: 5;
    display: flex;
    flex-direction: column;
    gap: 10px;
    .middle-header {
      padding: 10px;
      background-color: #ffffff20;
      .title,
      .desc {
        display: flex;
        align-items: center;
        p {
          flex: 1;
          text-align: center;
          font-size: 40px;
          color: #ffd500;
        }
      }
      .title {
        position: relative;
        border: #f0f0f01a 1px solid;
        p:nth-child(1) {
          position: relative;
          &::after {
            content: '';
            width: 2px;
            height: 80%;
            background-color: #f0f0f01a;
            position: absolute;
            top: 50%;
            right: 0;
            transform: translateY(-50%);
          }
        }
        &::before {
          content: '';
          width: 10px;
          height: 10px;
          position: absolute;
          top: 0;
          left: 0;
          border: 2px solid blueviolet;
          border-right: transparent;
          border-bottom: transparent;
        }
        &::after {
          content: '';
          width: 10px;
          height: 10px;
          position: absolute;
          bottom: 0;
          right: 0;
          border: 2px solid blueviolet;
          border-top: transparent;
          border-left: transparent;
        }
      }
      .desc {
        margin-top: 10px;
        p {
          font-size: 18px;
          color: #f0f0f0;
        }
      }
    }
    .middle-body {
      height: 100%;
      padding: 10px;
      background-color: #ffffff20;
      position: relative;
      .global {
        width: 518px;
        height: 518px;
        background: url('../assets/global.png') no-repeat 100% 100%;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        opacity: 0.4;
      }
      .stars {
        width: 643px;
        height: 643px;
        background: url('../assets/stars.png');
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        animation: rotate360 10s linear infinite;
      }
      .line {
        width: 566px;
        height: 566px;
        background: url('../assets/line.png');
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        animation: rotate360 10s linear infinite reverse;
      }
      .map-chart {
        width: 100%;
        height: 100%;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
      }
    }
  }
}
</style>