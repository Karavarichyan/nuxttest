<template>
  <div class="p-6 max-w-3xl mx-auto">
    <input
      v-model="input"
      type="text"
      placeholder="exemple: 5, 10, 15"
      class="w-full mb-4 px-4 py-2 border rounded"
    />
    <button
      @click="startVisualization"
      class="px-4 py-2 bg-green-500 text-white rounded hover:bg-green-600"
    >
      sort
    </button>
    <div>
      sample for copying
      <div>
        23, 87, 45, 12, 67, 39, 92, 15, 76, 53, 8, 100, 34, 61, 29, 70, 49, 6,
        81, 18
      </div>
    </div>
    <div class="mt-8 h-[300px] flex items-end gap-1 bg-gray-100 p-2 rounded">
      <div
        v-for="(num, index) in numbers"
        :key="index"
        class="flex-1 relative transition-all duration-300 ease-in-out rounded"
        :class="getBarColor(num)"
        :style="{ height: `${(num / maxValue) * 100}%` }"
      >
        <span class="absolute bottom-0 w-full text-center text-white text-xs">{{ num }}</span>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, nextTick } from 'vue'

const input = ref('')
const numbers = ref<number[]>([])

const maxValue = computed(() => {
  return numbers.value.length ? Math.max(...numbers.value) : 1
})

function getBarColor(num: number): string {
  const ratio = num / maxValue.value
  if (ratio > 0.8) return 'bg-red-500'
  if (ratio > 0.6) return 'bg-pink-500'
  if (ratio > 0.4) return 'bg-purple-500'
  if (ratio > 0.2) return 'bg-blue-500'
  return 'bg-blue-300'
}

function delay(ms: number) {
  return new Promise(resolve => setTimeout(resolve, ms))
}

async function quickSortNonMutating(arr: number[]): Promise<number[]> {
  if (arr.length <= 1) {
    return arr
  }

  const pivot = arr[0]
  const left: number[] = []
  const right: number[] = []
  const equal: number[] = []

  for (let i = 0; i < arr.length; i++) {
    const num = arr[i]
    if (num < pivot) {
      left.push(num)
    } else if (num > pivot) {
      right.push(num)
    } else {
      equal.push(num)
    }

    numbers.value = [...left, ...equal, ...right]
    await nextTick()
    await delay(50);
  }

  const sortedLeft = await quickSortNonMutating(left)
  const sortedRight = await quickSortNonMutating(right)

  const result = [...sortedLeft, ...equal, ...sortedRight]

  numbers.value = [...result]
  await nextTick()
  await delay(100);

  return result
}

async function startVisualization() {
  const arr = input.value
    .split(',')
    .map(i => parseInt(i.trim()))
    .filter(n => !isNaN(n))

  if (arr.length === 0) {
    numbers.value = []
    return
  }

  const initialNumbers = [...arr]
  numbers.value = [...initialNumbers]
  await nextTick()

  const sortedArray = await quickSortNonMutating([...initialNumbers])

  numbers.value = sortedArray
}
</script>
