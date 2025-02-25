<template>
  <footer class="bg-gray-800 px-4 py-8 text-white">
    <div class="container mx-auto">
      <!-- Main footer content -->
      <div class="mb-8 grid grid-cols-1 gap-8 md:grid-cols-2 lg:grid-cols-4">
        <!-- Column 1: About -->
        <div>
          <h3 class="mb-4 text-xl font-bold">
            About Us
          </h3>
          <p class="text-gray-300">
            We're dedicated to providing quality products and services to our customers worldwide.
          </p>
        </div>

        <!-- Column 2: Quick Links -->
        <div>
          <h3 class="mb-4 text-xl font-bold">
            Quick Links
          </h3>
          <ul class="space-y-2">
            <li
              v-for="(link, index) in navLinks"
              :key="index"
            >
              <a
                :href="link.url"
                class="text-gray-300 transition hover:text-white"
              >{{ link.name }}</a>
            </li>
          </ul>
        </div>

        <!-- Column 3: Contact Info -->
        <div>
          <h3 class="mb-4 text-xl font-bold">
            Contact Us
          </h3>
          <address class="not-italic text-gray-300">
            <p>123 Business Street</p>
            <p>City, State 12345</p>
            <p class="mt-2">
              Email: <a
                href="mailto:info@example.com"
                class="transition hover:text-white"
              >info@example.com</a>
            </p>
            <p>Phone: (123) 456-7890</p>
          </address>
        </div>

        <!-- Column 4: Newsletter Signup -->
        <div>
          <h3 class="mb-4 text-xl font-bold">
            Newsletter
          </h3>
          <p class="mb-2 text-gray-300">
            Stay updated with our latest news and offers.
          </p>
          <form @submit.prevent="submitNewsletterForm">
            <div class="flex flex-col space-y-2">
              <input
                v-model="email"
                type="email"
                placeholder="Your email address"
                class="rounded bg-gray-700 px-4 py-2 text-white focus:outline-none focus:ring-2 focus:ring-blue-500"
                required
              >
              <div
                v-if="emailError"
                class="text-sm text-red-400"
              >
                {{ emailError }}
              </div>
              <button
                type="submit"
                class="rounded bg-blue-600 px-4 py-2 text-white transition hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500"
              >
                Subscribe
              </button>
            </div>
          </form>
        </div>
      </div>

      <!-- Divider -->
      <div class="mb-4 border-t border-gray-700" />

      <!-- Bottom footer with copyright -->
      <div class="flex flex-col items-center justify-between md:flex-row">
        <p class="text-gray-400">
          &copy; {{ currentYear }} Your Company. All rights reserved.
        </p>
        <div class="mt-4 flex space-x-4 md:mt-0">
          <a
            v-for="(social, index) in socialLinks"
            :key="index"
            :href="social.url"
            :aria-label="social.name"
            class="text-gray-400 transition hover:text-white"
          >
            <span v-html="social.icon" />
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
// State
const email = ref('')
const emailError = ref('')
const currentYear = computed(() => new Date().getFullYear())

const navLinks = ref([
  { name: 'Home', url: '#' },
  { name: 'Services', url: '#services' },
  { name: 'About', url: '#about' },
  { name: 'Contact', url: '#contact' },
])

const socialLinks = ref([
  {
    name: 'Facebook',
    url: '#',
    icon: '<svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M22 12c0-5.523-4.477-10-10-10S2 6.477 2 12c0 4.991 3.657 9.128 8.438 9.878v-6.987h-2.54V12h2.54V9.797c0-2.506 1.492-3.89 3.777-3.89 1.094 0 2.238.195 2.238.195v2.46h-1.26c-1.243 0-1.63.771-1.63 1.562V12h2.773l-.443 2.89h-2.33v6.988C18.343 21.128 22 16.991 22 12z"/></svg>',
  },
  {
    name: 'Twitter',
    url: '#',
    icon: '<svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M8.29 20.251c7.547 0 11.675-6.253 11.675-11.675 0-.178 0-.355-.012-.53A8.348 8.348 0 0022 5.92a8.19 8.19 0 01-2.357.646 4.118 4.118 0 001.804-2.27 8.224 8.224 0 01-2.605.996 4.107 4.107 0 00-6.993 3.743 11.65 11.65 0 01-8.457-4.287 4.106 4.106 0 001.27 5.477A4.072 4.072 0 012.8 9.713v.052a4.105 4.105 0 003.292 4.022 4.095 4.095 0 01-1.853.07 4.108 4.108 0 003.834 2.85A8.233 8.233 0 012 18.407a11.616 11.616 0 006.29 1.84"/></svg>',
  },
  {
    name: 'Instagram',
    url: '#',
    icon: '<svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 100 12.324 6.162 6.162 0 000-12.324zM12 16a4 4 0 110-8 4 4 0 010 8zm6.406-11.845a1.44 1.44 0 100 2.881 1.44 1.44 0 000-2.881z"/></svg>',
  },
])

// Methods
const submitNewsletterForm = () => {
  // Email validation
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  if (!emailRegex.test(email.value)) {
    emailError.value = 'Please enter a valid email address.'
    return
  }

  emailError.value = ''
  // Here you would typically send the form data to your server
  alert('Thank you for subscribing to our newsletter!')
  email.value = ''
}
</script>

<style scope>

</style>
