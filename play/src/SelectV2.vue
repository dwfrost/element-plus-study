<template>
  select-v2:
  <el-select-v2
    v-model="value"
    :options="props.options"
    placeholder="select-v2"
    size="large"
  />
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
console.log('v2-created', t1)
onMounted(() => {
  const t2 = Date.now()
  console.log('v2-mounted', t2)
  console.log('v2-dom渲染耗时', t2 - t1)
  time.value = t2 - t1
})
</script>
<style lang="scss" scoped></style>
