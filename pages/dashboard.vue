<template>
    <div class="p-4">
      <h2 class="text-xl font-bold mb-4">Inventory Dashboard</h2>
  
      <label class="block mb-2">
        Filter by category:
        <select v-model="selectedCategory" class="border p-1 ml-2 rounded">
          <option v-for="cat in categories" :key="cat" :value="cat">{{ cat }}</option>
        </select>
      </label>

      <div class="flex flex-col items-center justify-center md:mt-20 mt-10 md:gap-20 gap-12">
        <div class="w-full max-w-2xl h-[500px] bg-white shadow rounded md:p-8 p-5">
          <h3 class="text-center md:text-2xl text-lg font-semibold mb-5">Pie Chart</h3>
          <Pie :data="chartData" :options="chartOptions" />
        </div>
      
        <div class="w-full max-w-2xl h-[300px] bg-white shadow rounded p-2">
          <h3 class="text-center md:text-2xl text-lg font-semibold mb-5">Bar Chart</h3>
          <Bar :data="chartData" :options="chartOptions" />
        </div>
      
        <div class="w-full max-w-2xl h-[500px] bg-white shadow rounded p-2">
          <h3 class="text-center md:text-2xl text-lg font-semibold mb-5">Doughnut Chart</h3>
          <Doughnut :data="chartData" :options="chartOptions" />
        </div>
      </div>
      </div>
  </template>
  
  
  <script setup>
import { ref, computed } from 'vue'
import { useInventory } from '~/composables/useInventory'
import { Chart as ChartJS, Title, Tooltip, Legend, ArcElement, BarElement, CategoryScale, LinearScale } from 'chart.js'
import { Pie, Bar, Doughnut } from 'vue-chartjs'

ChartJS.register(Title, Tooltip, Legend, ArcElement, BarElement, CategoryScale, LinearScale)

const { products } = useInventory()
const selectedCategory = ref('All')

const categories = computed(() => ['All', ...new Set(products.value.map(p => p.category))])

const filtered = computed(() =>
  selectedCategory.value === 'All' ? products.value : products.value.filter(p => p.category === selectedCategory.value)
)

const categoryCounts = computed(() => {
  const result = {}
  filtered.value.forEach(p => {
    result[p.category] = (result[p.category] || 0) + 1
  })
  return result
})

const chartData = computed(() => ({
  labels: Object.keys(categoryCounts.value),
  datasets: [{
    backgroundColor: ['#0ea5e9', '#facc15', '#10b981', '#ef4444', '#a855f7'],
    data: Object.values(categoryCounts.value)
  }]
}))

const chartOptions = {
  responsive: true,
  plugins: { legend: { position: 'bottom' } }
}
</script>
