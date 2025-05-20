<template>
    <div class="max-w-xl mx-auto p-4 bg-white shadow rounded mt-10">
      <h2 class="text-xl font-bold mb-4">Register New Product</h2>
  
      <form @submit.prevent="submit" class="space-y-4">
        <input v-model="form.name" placeholder="Product Name" class="border w-full p-2" required />
        <textarea v-model="form.description" placeholder="Description" class="border w-full p-2" />
        <input v-model.number="form.price" placeholder="Price" type="number" class="border w-full p-2" required />
        <input v-model.number="form.stock" placeholder="Initial Stock" type="number" class="border w-full p-2" />
        <input v-model="form.category" placeholder="Category" class="border w-full p-2" required />
        <input v-model="form.image" placeholder="Image URL" class="border w-full p-2" />
  
        <button type="submit" class="bg-blue-600 text-white px-4 py-2 rounded">Add Product</button>
      </form>
    </div>
  </template>
  
  <script setup>
import { ref } from 'vue'
import { useInventory } from '~/composables/useInventory'

const { addProduct } = useInventory()

const form = ref({
  name: '',
  description: '',
  price: 0,
  stock: 0,
  category: '',
  image: ''
})

// for registration
const submit = () => {
  if (form.value.name && form.value.price && form.value.category) {
    addProduct({ ...form.value })
    alert('Product added successfully!')
    form.value = { name: '', description: '', price: 0, stock: 0, category: '', image: '' }
  } else {
    alert('Please fill all required fields')
  }
}
</script>

