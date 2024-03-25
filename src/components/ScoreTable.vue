<script setup>
import { Info16Regular } from '@vicons/fluent'

import time from '@/static/time.json'
import best from '@/static/best.json'
import worst from '@/static/worst.json'
import average from '@/static/average.json'

defineProps({
  load: {
    type: Boolean,
    required: true
  }
})
defineExpose({
  update
})

let data_time = time['f1']
let data_best = best['f1']
let data_worst = worst['f1']
let data_average = average['f1']

function update(attr) {
  data_time = time[`${attr}`]
  data_best = best[`${attr}`]
  data_worst = worst[`${attr}`]
  data_average = average[`${attr}`]
}
</script>

<template>
  <n-spin :show="load">
    <n-card title="评估结果">
      <n-table :single-line="false" style="text-align: center">
        <thead>
          <tr>
            <th></th>
            <th>
              <div style="display: flex; justify-content: center; align-items: center">
                最优值
                <n-popover trigger="hover">
                  <template #trigger>
                    <n-icon size="20">
                      <Info16Regular />
                    </n-icon>
                  </template>
                  <p>独立运行30次结果中最接近函数最优解的值</p>
                </n-popover>
              </div>
            </th>
            <th>
              <div style="display: flex; justify-content: center; align-items: center">
                最差值
                <n-popover trigger="hover">
                  <template #trigger>
                    <n-icon size="20">
                      <Info16Regular />
                    </n-icon>
                  </template>
                  <p>独立运行30次结果中最远离函数最优解的值</p>
                </n-popover>
              </div>
            </th>
            <th>
              <div style="display: flex; justify-content: center; align-items: center">
                平均值
                <n-popover trigger="hover">
                  <template #trigger>
                    <n-icon size="20">
                      <Info16Regular />
                    </n-icon>
                  </template>
                  <p>独立运行30次的适应度平均值</p>
                </n-popover>
              </div>
            </th>
            <th>
              <div style="display: flex; justify-content: center; align-items: center">
                耗时
                <n-popover trigger="hover">
                  <template #trigger>
                    <n-icon size="20">
                      <Info16Regular />
                    </n-icon>
                  </template>
                  <p>求解问题所消耗的时间</p>
                </n-popover>
              </div>
            </th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>BSFPA</td>
            <td>{{ data_best[0] }}</td>
            <td>{{ data_worst[0] }}</td>
            <td>{{ data_average[0] }}</td>
            <td>{{ data_time[0] }}</td>
          </tr>
          <tr>
            <td>FPA</td>
            <td>{{ data_best[1] }}</td>
            <td>{{ data_worst[1] }}</td>
            <td>{{ data_average[1] }}</td>
            <td>{{ data_time[1] }}</td>
          </tr>
          <tr>
            <td>PSO</td>
            <td>{{ data_best[2] }}</td>
            <td>{{ data_worst[2] }}</td>
            <td>{{ data_average[2] }}</td>
            <td>{{ data_time[2] }}</td>
          </tr>
          <tr>
            <td>GA</td>
            <td>{{ data_best[3] }}</td>
            <td>{{ data_worst[3] }}</td>
            <td>{{ data_average[3] }}</td>
            <td>{{ data_time[3] }}</td>
          </tr>
          <tr>
            <td>FA</td>
            <td>{{ data_best[4] }}</td>
            <td>{{ data_worst[4] }}</td>
            <td>{{ data_average[4] }}</td>
            <td>{{ data_time[4] }}</td>
          </tr>
        </tbody>
      </n-table>
    </n-card>
    <template #description> loading </template>
  </n-spin>
</template>

<style scoped></style>
