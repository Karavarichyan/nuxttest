<template>
  <div class="max-w-xl mx-auto p-6">
    <h1 class="text-2xl font-bold mb-4">Two Sum</h1>
    <p class="mb-6">
Problem: Find the indices of two numbers in an array that add up to the target number.    </p>

    <form @submit.prevent="handleSubmit" class="space-y-4">
      <div>
        <label class="block mb-1 font-semibold">array numbers (,):</label>
       123 <input
          v-model="numsInput"
          type="text"
          placeholder="exemple: 2,7,11,15"
          class="w-full border rounded px-3 py-2"
          required
        />
      </div>

      <div>
        <label class="block mb-1 font-semibold">nuber</label>
        <input
          v-model.number="target"
          type="number"
          placeholder="exemple: 9"
          class="w-full border rounded px-3 py-2"
          required
        />
      </div>

      <button
        type="submit"
        class="bg-blue-600 text-white px-4 py-2 rounded hover:bg-blue-700"
      >
        serch index
      </button>
    </form>

    <div v-if="result" class="mt-6 p-4 bg-green-100 rounded">
      <h2 class="font-semibold mb-2">resualt :</h2>
      <p>index: {{ result.join(', ') }}</p>
    </div>

    <div v-if="error" class="mt-6 p-4 bg-red-100 rounded text-red-700">
      {{ error }}
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const numsInput = ref('')
const target = ref(null)
const result = ref(null)
const error = ref(null)

function twoSum(nums, target) {
  const map = new Map()
  for (let i = 0; i < nums.length; i++) {
    const x = target - nums[i]
    if (map.has(x)) {
      return [map.get(x), i]
    }
    map.set(nums[i], i)
  }
  return null
}

function handleSubmit() {
  error.value = null
  result.value = null

  try {
    const nums = numsInput.value
      .split(',')
      .map(n => n.trim())
      .filter(n => n !== '')
      .map(Number)

    if (nums.some(isNaN)) {
      error.value = 'Error: array contains non-numeric values.'
      return
    }

    if (nums.length < 2) {
      error.value = 'Error: The array must contain at least 2 numbers..'
      return
    }

    if (target.value === null || isNaN(target.value)) {
      error.value = 'Error: The target number is invalid.'
      return
    }

    const res = twoSum(nums, target.value)
    if (res) {
      result.value = res
    } else {
      error.value = 'Решение не найдено.'
    }
  } catch (e) {
    error.value = 'Произошла ошибка при обработке данных.'
  }
}
</script>
