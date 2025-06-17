<!-- components/Header.vue -->
<template>
  <nav class="bg-gray-800 p-4">
    <ul class="flex space-x-6 text-white">
      <li>
        <NuxtLink to="/" class="hover:text-yellow-400">Главная</NuxtLink>
      </li>
      <li>
        <NuxtLink to="/two-sum" class="hover:text-yellow-400">two-sum</NuxtLink>
      </li>
      <li>
        <NuxtLink to="/BubbleSort" class="hover:text-yellow-400">BubbleSort</NuxtLink>
      </li>
      <li>
        <NuxtLink to="/QuickSort" class="hover:text-yellow-400">QuickSort</NuxtLink>
      </li>
      <li>
        <NuxtLink to="/car-search" class="hover:text-yellow-400">car-search</NuxtLink>
      </li>
      <li>
        <NuxtLink to="QuickSortNotM"  class="hover:text-yellow-400">quickSortNonMutating </NuxtLink>
      </li>
    </ul>
  </nav>
</template>

<script setup>
</script>
