<script setup>
import { RouterLink } from 'vue-router';
import { PlusOutlined, MenuOutlined, CloseOutlined, LogoutOutlined } from '@ant-design/icons-vue';
import { ref } from 'vue';
import router from '@/router';

const isMobileMenuOpen = ref(false);

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value;
};

const logout = () => {
  localStorage.removeItem('jwt'); // Remove JWT from localStorage
  router.push('/signin'); // Redirect to login page
};
</script>

<template>
  <header class="fixed inset-x-0 top-0 z-50 bg-white shadow-md">
    <nav
      class="flex items-center justify-between px-4 py-3 sm:px-6 lg:px-8"
      aria-label="Global Navigation"
    >
      <!-- Logo -->
      <RouterLink
        to="/"
        class="text-xl font-semibold text-gray-800 hover:text-indigo-600"
      >
        User<span class="text-indigo-600">Manager</span>
      </RouterLink>

      <!-- Desktop Navigation -->
      <div class="hidden lg:flex items-center space-x-6">
        <RouterLink
          to="/"
          class="text-sm font-medium text-gray-700 hover:text-indigo-600"
        >
          Users
        </RouterLink>
        <RouterLink
          to="/create-user"
          class="text-sm font-medium text-gray-700 hover:text-indigo-600 flex items-center gap-1"
        >
          <PlusOutlined /> Create User
        </RouterLink>
      </div>

      <!-- Action Buttons -->
      <div class="hidden lg:flex items-center space-x-4">
        <button
          @click="logout"
          class="text-sm font-medium text-gray-700 hover:text-red-600 flex items-center gap-1"
        >
          <LogoutOutlined /> Log out
        </button>
      </div>

      <!-- Mobile Menu Toggle -->
      <button
        @click="toggleMobileMenu"
        class="lg:hidden text-gray-700 hover:text-indigo-600 focus:outline-none"
      >
        <MenuOutlined v-if="!isMobileMenuOpen" class="w-6 h-6" />
        <CloseOutlined v-if="isMobileMenuOpen" class="w-6 h-6" />
      </button>
    </nav>

    <!-- Mobile Navigation Menu -->
    <div
      v-if="isMobileMenuOpen"
      class="lg:hidden bg-gray-50 shadow-md absolute inset-x-0 top-full z-40 py-4 space-y-4 px-4 sm:px-6"
    >
      <RouterLink
        to="/"
        @click="toggleMobileMenu"
        class="block text-sm font-medium text-gray-700 hover:text-indigo-600"
      >
        Users
      </RouterLink>
      <RouterLink
        to="/create-user"
        @click="toggleMobileMenu"
        class=" text-sm font-medium text-gray-700 hover:text-indigo-600 flex items-center gap-1"
      >
        <PlusOutlined /> Create User
      </RouterLink>
      <button
        @click="() => { logout(); toggleMobileMenu(); }"
        class=" text-sm font-medium text-red-600 hover:text-red-800 flex items-center gap-1"
      >
        <LogoutOutlined /> Log out
      </button>
    </div>
  </header>
</template>

<style scoped>
/* Additional style improvements */
header {
  transition: all 0.3s ease-in-out;
}
nav {
  background-color: #fff;
}
button {
  transition: color 0.2s ease-in-out;
}
</style>
