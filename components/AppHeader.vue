<template>
    <div class="flex">
          <!-- Top Navbar -->
          <div class="py-3 px-6 md:px-10 border-b flex justify-between items-center fixed top-0 left-0 w-full bg-black shadow-lg text-white z-50">
            <!-- Left Icon / Logo -->
            <div class="flex items-center gap-3">
              <svg class="w-8 h-8 md:w-10 md:h-10 text-white" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                <path stroke-linecap="round" stroke-linejoin="round" d="M12 14l-4-4m0 0l4-4m-4 4h8"></path>
              </svg>
            </div>
      
            <!-- User Info (Responsive) -->
            <div class="flex items-center gap-3 md:gap-4">
  
              <!-- Notification Icon -->
              <div class="relative">
                <nuxt-link to='/notifications' class="focus:outline-none">
                  <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 md:w-7 md:h-7 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
                  </svg>
                </nuxt-link>
                <!-- Notification Dot -->
                <span class="absolute top-0 right-0 block h-2 w-2 rounded-full ring-2 ring-white bg-red-500"></span>
              </div>
              <div class="text-right">
                <p class="font-semibold text-xs md:text-sm">Forsit</p>
                <p class="text-xs text-gray-200">forsit@gmail.com</p>
              </div>
              <div class="relative">
                <img src="https://www.gravatar.com/avatar?d=mp" alt="User Avatar" class="w-8 h-8 md:w-10 md:h-10 rounded-full border-2 border-white shadow-md" />
              </div>
            </div>
          </div>
      <!-- Sidebar -->
      <aside 
        :class="[
          'fixed top-0 left-0 h-full w-56 bg-white shadow-2xl transition-transform duration-300 z-50',
          sidebarOpen ? 'translate-x-0' : '-translate-x-64',
          'md:translate-x-0'
        ]"
      >
        <!-- Logo -->
        <div class="px-6 py-3 border-b flex bg-black justify-center">
          <nuxt-link to="/">
            <p class="text-white text-4xl">Forsit</p>
          </nuxt-link>
        </div>
  
        <!-- Navigation Links -->
        <ul class="mt-6 text-gray-700">
          <!-- Dashboard Link -->
          <li> 
            <nuxt-link 
              to="/dashboard" 
              class="flex items-center gap-2 px-6 py-2 hover:bg-black hover:text-white font-semibold rounded-lg transition mx-4"
            >
              Dashboard
            </nuxt-link>
          </li>
          <!-- registration link. -->
                    <li> 
            <nuxt-link 
              to="/registration" 
              class="flex items-center gap-2 px-6 py-2 hover:bg-black hover:text-white font-semibold rounded-lg transition mx-4"
            >
              Registration
            </nuxt-link>
          </li>
        </ul>
  
        <!-- Logout Button -->
        <div class="absolute bottom-6 w-full px-6">
          <button @click="logout" class="w-full flex items-center gap-2 px-4 py-3 text-red-500 hover:bg-red-100 hover:text-red-700 rounded-lg">
            Logout
          </button>
        </div>
      </aside>
  
      <!-- Sidebar Toggle Button -->
      <button 
        @click="toggleSidebar" 
        class="fixed top-2 left-5 z-50 bg-black text-white p-2 rounded-lg shadow-lg md:hidden"
      >
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" viewBox="0 0 24 24">
          <path d="M3 12h18M3 6h18M3 18h18"></path>
        </svg>
      </button>
  
      <!-- Main Content -->
      <div :class="['flex-1 p-6 transition-all duration-300', sidebarOpen ? 'ml-56' : 'ml-0', 'md:ml-56']">
        <slot />
      </div>
  
      <!-- Mobile Overlay -->
      <div v-if="sidebarOpen" @click="toggleSidebar" class="fixed inset-0 bg-black opacity-50 md:hidden"></div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';

  const sidebarOpen = ref(false);
  const openDropdown = ref(null);

  
  const toggleSidebar = () => {
    sidebarOpen.value = !sidebarOpen.value;
  };
  
  // Function to toggle dropdown and close others
  const toggleDropdown = (menu, event) => {
    event.preventDefault(); // Stop default behavior of <details>
    openDropdown.value = openDropdown.value === menu ? null : menu;
  };
  </script>
  