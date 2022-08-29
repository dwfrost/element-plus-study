<template>
  select-v1:
  <el-select v-model="value" placeholder="select-v1" size="large">
    <el-option
      v-for="item in props.options"
      :key="item.value"
      :label="item.label"
      :value="item.value"
    />
  </el-select>
  DOM挂载耗时：{{ time }}ms
</template>
<script setup lang="ts">
import { onMounted, ref } from 'vue'

const props = defineProps({
  options: {
    type: Array,
    default: () => [],
  },
})
const value = ref('')
const time = ref(0)

const t1 = Date.now()
console.log('v1-created', t1)
onMounted(() => {
  const t2 = Date.now()
  console.log('v1-mounted', t2)
  console.log('v1-dom渲染耗时', t2 - t1)
  time.value = t2 - t1
})
</script>
<style lang="scss" scoped></style>
