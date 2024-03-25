<script setup>
import { ref } from 'vue'
// 引入 echarts 核心模块，核心模块提供了 echarts 使用必须要的接口。
import { use } from 'echarts/core'
// 引入柱状图图表，图表后缀都为 Chart
import { LineChart } from 'echarts/charts'
// 引入 Canvas 渲染器，注意引入 CanvasRenderer 或者 SVGRenderer 是必须的一步
import { CanvasRenderer } from 'echarts/renderers'
// 标签自动布局、全局过渡动画等特性
import { LabelLayout, UniversalTransition } from 'echarts/features'
// 引入提示框，标题，直角坐标系，数据集，内置数据转换器组件，组件后缀都为 Component
import {
  TitleComponent,
  TooltipComponent,
  GridComponent,
  DatasetComponent,
  TransformComponent,
  LegendComponent,
  DataZoomComponent
} from 'echarts/components'
import VChart from 'vue-echarts'

import data from '@/static/data.json'


// 注册必须的组件
use([
  CanvasRenderer,
  TitleComponent,
  TooltipComponent,
  GridComponent,
  DatasetComponent,
  TransformComponent,
  LabelLayout,
  UniversalTransition,
  LineChart,
  LegendComponent,
  DataZoomComponent
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

const image = ref(null)

var option = {
  animationDuration: 3000,
  dataset: [
    {
      id: 'dataset_raw',
      source: data,
    },
    {
      id: 'dataset_filtered',
      fromDatasetId: 'dataset_raw',
      transform: {
        type: 'filter',
        config: { dimension: 'fun_name', '=': 'f1' }
      }
    },
  ],

  title: {
    text: '在不同函数上的收敛曲线对比图'
  },

  tooltip: {
    trigger: 'axis'
  },
  legend: {
    data: ['BSFPA', 'FPA', 'PSO', 'GA', 'FA']
  },
  xAxis: {
    type: 'category',
    name: 'Iteration'
  },
  yAxis: {
    // name: 'Fitness Value'
  },
  dataZoom: [{
    type: 'slider',
    show: true,
    xAxisIndex: [0],
    start: 0,
    end: 100
  },
  {
    type: 'slider',
    show: true,
    yAxisIndex: [0],
    left: '93%',
    start: 0,
    end: 100
  },
  ],
  grid: {
    right: 100
  },
  series: [
    {
      name: 'BSFPA',
      datasetId: 'dataset_filtered',
      type: 'line',
      smooth: true,
      showSymbol: false,
      emphasis: {
        focus: 'series'
      },
      encode: {
        x: 'iteration',
        y: 'MFPA',
      }
    },
    {
      name: 'FPA',
      datasetId: 'dataset_filtered',
      type: 'line',
      smooth: true,
      showSymbol: false,
      emphasis: {
        focus: 'series'
      },
      encode: {
        x: 'iteration',
        y: 'FPA'
      }
    },
    {
      name: 'PSO',
      datasetId: 'dataset_filtered',
      type: 'line',
      smooth: true,
      showSymbol: false,
      emphasis: {
        focus: 'series'
      },
      encode: {
        x: 'iteration',
        y: 'PSO'
      }
    },
    {
      name: 'GA',
      datasetId: 'dataset_filtered',
      type: 'line',
      smooth: true,
      showSymbol: false,
      emphasis: {
        focus: 'series'
      },
      encode: {
        x: 'iteration',
        y: 'GA'
      }
    },
    {
      name: 'FA',
      datasetId: 'dataset_filtered',
      type: 'line',
      smooth: true,
      showSymbol: false,
      emphasis: {
        focus: 'series'
      },
      encode: {
        x: 'iteration',
        y: 'FA'
      }
    }
  ]
};

function update(attr) {
  option.dataset[1].transform.config =
    { dimension: 'fun_name', '=': attr }
  option.title.text = '在函数 ' + attr + ' 上的收敛曲线对比图'
  image.value.clear()
  image.value.setOption(option)
}
</script>

<template>
  <v-chart :option="option" style="height: 540px" :loading="load" ref="image" />
</template>

<style scoped></style>
