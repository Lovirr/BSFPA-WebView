<script setup>
import { ref } from 'vue'
import data from '@/static/data.json'

const emit = defineEmits(['update'])

// function getLabel(value) {
//   for (let index = 0; index < options.length; index++) {
//     const element = options[index]
//     if (element.value === value) {
//       return element.label
//     }
//     for (let i = 0; i < element.children.length; i++) {
//       const child = element.children[i]
//       if (child.value === value) {
//         return child.label
//       }
//     }
//   }
// }

function changeModel() {
  if (!attrs.value) {
    showModal_403.value = true
    message_403.value = '参数空着可不好哦~'
    return
  }
  let find = false
  const attr = attrs.value
  for (let index = 0; index < data.length; index++) {
    const element = data[index]
    if (element[0] === attr) {
      find = true
      break
    }
  }
  if (!find) {
    showModal.value = true
    return
  }
  emit('update', attr)
}


const attrs = ref(null)
const options = [
      { label: 'Function1', value: 'f1' },
      { label: 'Function2', value: 'f2' },
      { label: 'Function3', value: 'f3' },
      { label: 'Function4', value: 'f4' },
      { label: 'Function5', value: 'f5' },
      { label: 'Function6', value: 'f6' },
      { label: 'Function7', value: 'f7' },
      { label: 'Function8', value: 'f8' },
      { label: 'Function9', value: 'f9' },
      { label: 'Function10', value: 'f10' },
      { label: 'Function11', value: 'f11' },
      { label: 'Function12', value: 'f12' },
      { label: 'Function13', value: 'f13' },
      { label: 'Function14', value: 'f14' },
      { label: 'Function15', value: 'f15' },
      { label: 'Function16', value: 'f16' },
      { label: 'Function17', value: 'f17' },
      { label: 'Function18', value: 'f18' },
      { label: 'Function19', value: 'f19' },
      { label: 'Function20', value: 'f20' }
]

const showModal = ref(false)
const showModal_403 = ref(false)
const message_403 = ref('')
</script>

<template>
  <n-card title="测试函数选择">
    <div style="display: block; justify-content: space-between">
      <n-form-item label="测试函数" style="flex-grow: 1; margin-right: 30px">
        <n-cascader v-model:value="attrs" :options="options" />
      </n-form-item>
    </div>
    <br /><br />
    <div style="display: flex; justify-content: flex-end">
      <n-button @click="changeModel()" type="primary">开始测试</n-button>
    </div>
  </n-card>
  <n-modal v-model:show="showModal">
    <n-card style="width: 600px">
      <n-result status="404" title="攻击模型中" description="数据还未准备好，待会再来吧~">
        <template #footer>
          <n-button @click="showModal = false">换个参数吧</n-button>
        </template>
      </n-result>
    </n-card>
  </n-modal>
  <n-modal v-model:show="showModal_403">
    <n-card style="width: 600px">
      <n-result status="403" title="参数异常" :description="message_403">
        <template #footer>
          <n-button @click="showModal_403 = false">我知道啦</n-button>
        </template>
      </n-result>
    </n-card>
  </n-modal>
</template>

<style scoped></style>
