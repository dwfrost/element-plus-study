<template>
  <div class="play-container">
    <div class="item">
      <el-button @click="showV1"
        >{{ v1Show ? '隐藏' : '显示' }}select-v1</el-button
      >
    </div>
    <div class="item">
      <el-button @click="showV2"
        >{{ v2Show ? '隐藏' : '显示' }}select-v2</el-button
      >
    </div>
    <div class="item">
      数据量：
      <el-select v-model="total" @change="onChange">
        <el-option
          v-for="item in totalOptions"
          :key="item"
          :label="item"
          :value="item"
        /> </el-select
      >条
    </div>
    <template v-if="show">
      <div v-if="v1Show" class="item">
        <SelectV1 :options="options" />
      </div>
      <div v-if="v2Show" class="item">
        <SelectV2 :options="options" />
      </div>
    </template>
  </div>
</template>

<script setup lang="ts">
import { computed, nextTick, onMounted, ref } from 'vue'
import SelectV1 from './SelectV1.vue'
import SelectV2 from './SelectV2.vue'

const initials = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']

const total = ref(10000)
const totalOptions = [10, 100, 1000, 10000, 50000]
const onChange = () => {
  show.value = false
  nextTick(() => {
    show.value = true
  })
}

const show = ref(true)
const options = computed(() => {
  return Array.from({ length: total.value }).map((_, idx) => ({
    value: `Option ${idx + 1}`,
    label: `${initials[idx % 10]}${idx}`,
  }))
})
const t1 = Date.now()
console.log('created', t1)
onMounted(() => {
  const t2 = Date.now()
  console.log('mounted', t2)
  console.log('dom渲染耗时', t2 - t1)
})

const v2Show = ref(false)
const showV2 = () => {
  v2Show.value = !v2Show.value
}
const v1Show = ref(false)
const showV1 = () => {
  v1Show.value = !v1Show.value
}
</script>

<style lang="scss">
html,
body {
  width: 100vw;
  height: 100vh;
  margin: 0;
  #play {
    height: 100%;
    width: 100%;
    .play-container {
      height: 100%;
      width: 100%;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      .item {
        margin: 10px 0;
      }
    }
  }
}
</style>
