<template>
    <div class="flex justify-between mx-auto w-full min-h-screen z-10">
      <main class="bg-white w-full mx-auto">
        <div class="container p-4">
          <table class="table-auto w-full border-collapse border border-gray-200 text-black md:text-sm text-xs bg-white rounded">
            <thead>
              <tr class="bg-black text-white md:text-base text-sm">
                <th class="px-4 py-2 rounded-l">Product ID</th>
                <th class="px-4 py-2">Title</th>
                <th class="px-4 py-2">Category</th>
                <th class="px-4 py-2 rounded-r">Price</th>
              </tr>
            </thead>
            <tbody>
              <tr
                v-for="product in filteredProducts"
                :key="product.id"
                @click="openModal(product)"
                class="hover:bg-gray-50 text-center cursor-pointer"
              >
                <td class="border-b border-gray-200 px-4 py-2 rounded-l">{{ product.id }}</td>
                <td class="border-b border-gray-200 px-4 py-2">{{ product.title }}</td>
                <td class="border-b border-gray-200 px-4 py-2">{{ product.category }}</td>
                <td class="border-b border-gray-200 px-4 py-2 rounded-r">${{ product.price }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </main>
  
      <!-- Modal -->
      <div v-if="modalData" class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center">
        <div class="bg-white rounded-lg shadow-lg w-[400px] p-6">
          <div class="flex items-center justify-between mb-4">
            <div class="ml-4 bg-black p-2 flex justify-center mx-auto rounded text-center">
              <h3 class="text-base text-center font-bold text-white">Product Details</h3>
            </div>
            <button @click="closeModal" class="text-gray-500 hover:text-gray-800">&times;</button>
          </div>
          <div class="text-center">
            <h4 class="text-lg font-semibold mb-2">{{ modalData.title }}</h4>
            <p class="text-gray-600 mb-1">{{ modalData.description }}</p>
            <p class="text-sm">Price: ${{ modalData.price }}</p>
          </div>
        </div>
      </div>
    </div>
  </template>

  <script setup>
  import { ref, computed } from 'vue'
  import { useInventory } from '~/composables/useInventory'
  
//   inventry data
  const { products } = useInventory()
  const modalData = ref(null)
  
  // Filtering
  const filteredProducts = computed(() => products.value)
  
  // Modal
  const openModal = (product) => {
    modalData.value = product
  }
  
  const closeModal = () => {
    modalData.value = null
  }
  </script>
  