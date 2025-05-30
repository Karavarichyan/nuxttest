<template>
  <div class="max-w-xl mx-auto mt-10 font-sans">
    <h1 class="text-2xl font-bold mb-4">Search Cars</h1>
    <input
      type="text"
      v-model="query"
      placeholder="Brand, Model or Year"
      class="w-full p-2 text-base mb-4 border rounded"
    />

    <ul>
      <li
        v-for="(car, index) in filteredCars"
        :key="index"
        class="mb-1"
      >
        {{ car.brand }} {{ car.model }} — {{ car.year }}
      </li>
      <li v-if="filteredCars.length === 0">Cars not found</li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

type Car = {
  brand: string
  model: string
  year: number
}

const cars: Car[] = [
  { brand: 'Toyota', model: 'Corolla', year: 2018 },
  { brand: 'Honda', model: 'Civic', year: 2020 },
  { brand: 'Ford', model: 'Focus', year: 2017 },
  { brand: 'BMW', model: 'X5', year: 2022 },
]

const query = ref('')

const filteredCars = computed(() => {
  const value = query.value.toLowerCase()
  if (!value) return cars

  return cars.filter(({ brand, model, year }) => {
    return (
      brand.toLowerCase().includes(value) ||
      model.toLowerCase().includes(value) ||
      year.toString().includes(value)
    )
  })
})
</script>
