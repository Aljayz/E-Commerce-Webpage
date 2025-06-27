<template>
  <div id="MainLayout" class="flex flex-col h-screen">
    <header 
      ref="header"
      class="bg-black text-white p-4 fixed top-0 left-0 right-0 z-50 transition-all duration-300"
      :class="{ '-translate-y-full': !showHeader, 'shadow-lg': !showHeader }"
    >
      <nav class="flex items-center justify-between">
        <NuxtLink to="/" class="hover:grayscale-75"><img src="~/assets/img/JOBARSEVENTLOGO.png" alt="JOBARS" class="h-15 inline-block mr-4"></NuxtLink>
        
        <!-- Desktop Navigation (hidden on mobile) -->
        <ul class="hidden md:flex space">
            <li class="mr-6 relative group">
                <NuxtLink to="/" class="text-white hover:text-gray-400 relative inline-block py-2">
                Home
                <span class="absolute bottom-0 left-1/2 w-0 h-0.5 bg-white transition-all duration-300 group-hover:w-full group-hover:left-0"></span>
                </NuxtLink>
            </li>
            <li class="mr-6 relative group">
                <NuxtLink to="events" class="text-white hover:text-gray-400 relative inline-block py-2">
                Events
                <span class="absolute bottom-0 left-1/2 w-0 h-0.5 bg-white transition-all duration-300 group-hover:w-full group-hover:left-0"></span>
                </NuxtLink>
            </li>
            <li class="mr-6 relative group">
                <NuxtLink to="about" class="text-white hover:text-gray-400 relative inline-block py-2">
                About Us
                <span class="absolute bottom-0 left-1/2 w-0 h-0.5 bg-white transition-all duration-300 group-hover:w-full group-hover:left-0"></span>
                </NuxtLink>
            </li>
            <li class="mr-6 relative group">
                <NuxtLink to="contact" class="text-white hover:text-gray-400 relative inline-block py-2">
                Contact
                <span class="absolute bottom-0 left-1/2 w-0 h-0.5 bg-white transition-all duration-300 group-hover:w-full group-hover:left-0"></span>
                </NuxtLink>
            </li>
        </ul>
        
        <!-- Mobile Hamburger Button (hidden on desktop) -->
        <button 
          @click="isMobileMenuOpen = !isMobileMenuOpen"
          class="md:hidden text-white focus:outline-none"
          aria-label="Toggle menu"
        >
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path 
              stroke-linecap="round" 
              stroke-linejoin="round" 
              stroke-width="2" 
              :d="isMobileMenuOpen ? 'M6 18L18 6M6 6l12 12' : 'M4 6h16M4 12h16M4 18h16'"
            />
          </svg>
        </button>
      </nav>
      
      <!-- Mobile Menu (hidden on desktop) -->
      <div 
        v-if="isMobileMenuOpen"
        class="md:hidden bg-black transition-all duration-300 ease-in-out"
        :class="{ 'max-h-0 overflow-hidden': !isMobileMenuOpen, 'max-h-screen': isMobileMenuOpen }"
      >
        <ul class="flex flex-col space-y-3 p-4">
          <li><a class="text-white hover:text-gray-400 block"><NuxtLink to="home" @click="isMobileMenuOpen = false">Home</NuxtLink></a></li>
          <li><a class="text-white hover:text-gray-400 block"><NuxtLink to="products" @click="isMobileMenuOpen = false">Products</NuxtLink></a></li>
          <li><a class="text-white hover:text-gray-400 block"><NuxtLink to="about" @click="isMobileMenuOpen = false">About Us</NuxtLink></a></li>
          <li><a class="text-white hover:text-gray-400 block"><NuxtLink to="contact" @click="isMobileMenuOpen = false">Contact</NuxtLink></a></li>
        </ul>
      </div>
    </header>
    
    <main class="flex-1 pt-16">
      <slot/>
    </main>
    
    <footer class="bg-black text-white p-4 text-center">
      © June 2025 JOBARSEVENTLOGO. All rights reserved.
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const showHeader = ref(true);
const lastScrollPosition = ref(0);
const header = ref(null);
const isMobileMenuOpen = ref(false);

const onScroll = () => {
  const currentScrollPosition = window.pageYOffset || document.documentElement.scrollTop;
  
  // For mobile or negative scrolling
  if (currentScrollPosition < 0) {
    return;
  }
  
  // If the difference between the
  // current scroll position and last scroll position is less than some offset
  if (Math.abs(currentScrollPosition - lastScrollPosition.value) < 60) {
    return;
  }
  
  // Show header if scrolling up or at top of page
  if (currentScrollPosition < lastScrollPosition.value || currentScrollPosition <= 0) {
    showHeader.value = true;
  } else {
    // Hide header if scrolling down
    showHeader.value = false;
    isMobileMenuOpen.value = false; // Close mobile menu when scrolling down
  }
  
  lastScrollPosition.value = currentScrollPosition;
};

onMounted(() => {
  window.addEventListener('scroll', onScroll);
});

onUnmounted(() => {
  window.removeEventListener('scroll', onScroll);
});
</script>

<style>
/* Smooth scrolling behavior */
html {
  scroll-behavior: smooth;
}

/* Transition for mobile menu */
.mobile-menu-enter-active,
.mobile-menu-leave-active {
  transition: max-height 0.3s ease;
}
.mobile-menu-enter-from,
.mobile-menu-leave-to {
  max-height: 0;
}
.mobile-menu-enter-to,
.mobile-menu-leave-from {
  max-height: 500px;
}
</style>
