<template>
  <header
    class="sticky left-0 top-0 z-50 w-full transition-all duration-300"
    :class="{ 'bg-white shadow-md': isScrolled, 'bg-transparent': !isScrolled }"
  >
    <div class="container mx-auto px-4">
      <div class="flex h-16 items-center justify-between">
        <!-- Logo -->
        <div class="shrink-0">
          <nuxt-link
            to="/"
            class="text-xl font-bold"
            :class="{ 'text-gray-800': isScrolled, 'text-blue-600': !isScrolled }"
          >
            Nuxt Template Starter
          </nuxt-link>
        </div>

        <!-- Desktop Navigation -->
        <nav class="hidden space-x-8 md:flex">
          <a
            v-for="(link, index) in navLinks"
            :key="index"
            :href="link.url"
            class="py-2 transition-colors duration-300"
            :class="[
              link.isActive
                ? 'border-b-2 border-blue-600 font-medium text-blue-600'
                : 'text-gray-600 hover:text-blue-600',
            ]"
          >
            {{ link.name }}
          </a>
        </nav>

        <!-- Mobile Menu Button -->
        <div class="md:hidden">
          <button
            class="rounded-md p-2 text-gray-800 focus:outline-none"

            @click="toggleMobileMenu"
          >
            <svg
              class="size-6"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                v-if="!isMobileMenuOpen"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M4 6h16M4 12h16M4 18h16"
              />
              <path
                v-else
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </button>
        </div>
      </div>
    </div>

    <!-- Mobile Menu -->
    <div
      v-show="isMobileMenuOpen"
      class="overflow-hidden bg-white shadow-lg transition-all duration-300 ease-in-out md:hidden"
      :class="{ 'max-h-64': isMobileMenuOpen, 'max-h-0': !isMobileMenuOpen }"
    >
      <div class="space-y-1 px-4 py-2">
        <a
          v-for="(link, index) in navLinks"
          :key="index"
          :href="link.url"
          class="block rounded-md px-3 py-2 text-base font-medium transition-colors duration-200"
          :class="[
            link.isActive
              ? 'bg-blue-100 text-blue-600'
              : 'text-gray-600 hover:bg-gray-100 hover:text-blue-600',
          ]"
        >
          {{ link.name }}
        </a>
      </div>
    </div>
  </header>
</template>

<script setup lang="ts">
// State
const isScrolled = ref(false)
const isMobileMenuOpen = ref(false)
const navLinks = ref([
  { name: 'Home', url: '#', isActive: true },
  { name: 'Services', url: '#services', isActive: false },
  { name: 'About', url: '#about', isActive: false },
  { name: 'Contact', url: '#contact', isActive: false },
])

// Methods
const handleScroll = () => {
  isScrolled.value = window.scrollY > 10
}

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}

// Lifecycle hooks
onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  // Check scroll position on initial mount
  handleScroll()
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
</style>
