<script setup>
import num from '@/static/model-info.json'

defineProps({
  load: {
    type: Boolean,
    required: true
  }
})

defineExpose({
  update
})

let data = num['f1']

function update(attr) {
  data = num[`${attr}`]
}

</script>

<template>
  <n-spin :show="load">
    <n-card title="模型参数" style="height: 300px">
      <n-grid>
        <n-gi span="12">
          <n-statistic label="训练函数" tabular-nums>
            <n-number-animation :from="0" :to=23 />
            <template #suffix> 个 </template>
          </n-statistic>
        </n-gi>
        <n-gi span="12">
          <n-statistic label="测试算法" tabular-nums>
            <n-number-animation :from="0" :to="5" />
            <template #suffix> 种 </template>
          </n-statistic>
        </n-gi>
      </n-grid>
      <n-grid>
        <n-gi span="12">
          <n-statistic label="迭代次数" tabular-nums>
            <n-number-animation :from="0" :to="data[0]" />
            <template #suffix> 次 </template>
          </n-statistic>
        </n-gi>
        <n-gi span="12">
          <n-statistic label="种群数" tabular-nums>
            <n-number-animation :from="0" :to="20" />
            <template #suffix> 组 </template>
          </n-statistic>
        </n-gi>
        <n-gi span="12">
          <n-statistic label="函数维度" tabular-nums>
            <n-number-animation :from="0" :to="data[1]" />
            <template #suffix> 维 </template>
          </n-statistic>
        </n-gi>
        <n-gi span="12">
          <n-statistic label="独立运行" tabular-nums>
            <n-number-animation :from="0" :to="30" />
            <template #suffix> 次 </template>
          </n-statistic>
        </n-gi>
      </n-grid>
    </n-card>
    <template #description> loading </template>
  </n-spin>
</template>

<style scoped></style>
