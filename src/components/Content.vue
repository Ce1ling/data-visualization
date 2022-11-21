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
        <div class="title">
          <p>423891</p>
          <p>123456</p>
        </div>
        <div class="desc">
          <p>数据总量</p>
          <p>区间总量</p>
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
      <MiniChart :list="rightList" />
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
        border: 1px solid red;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
      }
    }
  }
}
</style>