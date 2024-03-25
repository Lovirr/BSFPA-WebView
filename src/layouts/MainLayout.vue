<script setup>
import { ref } from 'vue'
import EChartImage from '@/components/EChartImage.vue'
import ModelControl from '@/components/ModelControl.vue'
import ModelInfo from '@/components/ModelInfo.vue'
import ScoreTable from '@/components/ScoreTable.vue'
import DataDistribution from '@/components/DataRank.vue'

const load = ref(false)
const image = ref(null)
const score = ref(null)
const info = ref(null)
const distribution = ref(null)

function update(attr) {
  load.value = true
  setTimeout(() => {
    image.value.update(attr)
    distribution.value.update(attr)
    info.value.update(attr)
    score.value.update(attr)
    load.value = false
  }, 1000)
}
</script>

<template>
  <n-grid x-gap="12" style="margin-top: 5px">
    <n-gi span="6">
      <model-control @update="update" style="height: 300px; justify-content: center" />
    </n-gi>
    <n-gi span="12">
      <n-gradient-text :size="70" type="success" class="title">
        基于仿生搜索的<br />花朵授粉算法可视化
      </n-gradient-text>
    </n-gi>
    <n-gi span="6">
      <model-info :load="load" ref="info" />
    </n-gi>
  </n-grid>
  <n-grid x-gap="1" style="margin-left: 8px">
    <n-gi span="18">
      <e-chart-image :load="load" ref="image" />
    </n-gi>
    <n-gi span="6">
      <br /><br /><br />
      <data-distribution :load="load" ref="distribution" />
    </n-gi>
  </n-grid>
  <br />
  <n-grid x-gap="12" style="margin-top: 5px">
    <n-gi span="24">
      <score-table :load="load" ref="score" />
    </n-gi>
  </n-grid>
</template>

<style scoped>
.title {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 300px;
  background-image: -webkit-linear-gradient(200deg, rgb(69, 101, 216) 30%, rgb(66, 159, 236));
}
</style>
