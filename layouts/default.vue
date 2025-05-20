<template>
    <div class="min-h-screen">
  
  
      <!-- App Header -->
      <AppHeader />
      <!-- Layout Wrapper -->
      <div class="flex">
        <!-- Main Content -->
        <div :class="['flex-1 pt-16 p-4 md:p-6 transition-all duration-300', sidebarOpen ? 'ml-64' : 'ml-0', 'md:ml-64']">
          <slot />
        </div>
      </div>
      <!-- Overlay for Mobile -->
      <div v-if="sidebarOpen" @click="toggleSidebar" class="fixed inset-0 bg-black opacity-50 md:hidden"></div>
    </div>
               <!-- footer seciton  -->
               <!-- <div class="md:ml-56 w-full">
                <Footer />
               </div> -->
  </template>
  
  <script setup>
//   useHead({
//     title: 'Forsit',
//     link: [{ rel: 'icon', type: 'image/png', href: '/favicon.png' }]
//   });
  import { ref } from "vue";
  
  const sidebarOpen = ref(false);
  
  const toggleSidebar = () => {
    sidebarOpen.value = !sidebarOpen.value;
  };
  
  </script>