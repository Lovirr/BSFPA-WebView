<script setup>
import { ref } from 'vue'
import { use } from 'echarts/core'
import { BarChart } from 'echarts/charts'
import { CanvasRenderer } from 'echarts/renderers'
import { LabelLayout, UniversalTransition } from 'echarts/features'
import {
  GridComponent,
  DatasetComponent,
  TransformComponent,
  LegendComponent
} from 'echarts/components'
import VChart from 'vue-echarts'

import min from '@/static/min-iteration.json'

// 注册必须的组件
use([
  CanvasRenderer,
  GridComponent,
  DatasetComponent,
  TransformComponent,
  LabelLayout,
  UniversalTransition,
  BarChart,
  LegendComponent
])

defineProps({
  load: {
    type: Boolean,
    required: true
  }
})

defineExpose({
  update
})

let data = [
  { value: 100, itemStyle: { color: '#5470C6' } },
  { value: 222, itemStyle: { color: '#91CC75' } },
  { value: 333, itemStyle: { color: '#FAC858' } },
  { value: 890, itemStyle: { color: '#73C0DE' } },
  { value: 590, itemStyle: { color: '#EE6666' } }
]

const distribution = ref(null)

function update(attr) {
  data = min[`${attr}`]
  option.series[0].data = [
    { value: data[0], itemStyle: { color: '#5470C6' } },
    { value: data[1], itemStyle: { color: '#91CC75' } },
    { value: data[2], itemStyle: { color: '#FAC858' } },
    { value: data[3], itemStyle: { color: '#73C0DE' } },
    { value: data[4], itemStyle: { color: '#EE6666' } }
  ]
  distribution.value.clear()
  distribution.value.setOption(option)
}

const option = {
  xAxis: {
    type: 'category',
    data: ['BSFPA', 'FPA', 'PSO', 'GA', 'FA']
  },
  yAxis: {},
  tooltip: {
    trigger: 'axis',
    axisPointer: {
      type: 'shadow'
    }
  },
  emphasis: {
    focus: 'series'
  },
  series: [
    {
      data: data,
      type: 'bar',
    }
  ]
}
</script>

<template>
  <n-card title="最小迭代次数" :loading="load">
    <v-chart :option="option" style="height: 400px ;width: 113%" :loading="load" ref="distribution" />
  </n-card>
</template>

<style scoped></style>
