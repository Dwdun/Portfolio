<template>
  <nav class="fixed top-0 left-0 right-0 z-50 w-full px-6 md:px-12 py-6 md:py-8 bg-transparent">
    <div class="grid grid-cols-2 md:grid-cols-3 items-start gap-4 uppercase tracking-[0.2em] text-xs sm:text-sm font-sans text-black">
      
      <!-- Left: Logo & Info -->
      <div class="flex flex-col space-y-1">
        <NuxtLink to="/" class="hover:opacity-70 transition-opacity font-semibold">
          INDEX, INFO
        </NuxtLink>
        <span class="hidden md:inline-block text-black/60">{{ profile?.name || 'Muhammad Faqih Shiam' }}</span>
      </div>

      <!-- Center: Time (Hidden on Mobile) -->
      <div class="hidden md:flex flex-col items-center space-y-1">
        <ClientOnly>
          <span class="font-serif text-xl sm:text-2xl tracking-normal">{{ currentTime }}</span>
        </ClientOnly>
        <span class="text-black/60">Bandung, ID</span>
      </div>

      <!-- Right: Links / Journal -->
      <div class="flex flex-col items-end space-y-1 relative">
        <button @click="mobileMenuOpen = !mobileMenuOpen" class="hover:opacity-70 transition-opacity font-semibold flex items-center gap-2">
          JOURNAL <span class="text-[0.6rem] transition-transform duration-300" :class="mobileMenuOpen ? 'rotate-180' : ''">▼</span>
        </button>
        
        <!-- Dropdown Menu -->
        <Transition
          enter-active-class="transition duration-300 ease-out"
          enter-from-class="transform -translate-y-2 opacity-0"
          enter-to-class="transform translate-y-0 opacity-100"
          leave-active-class="transition duration-200 ease-in"
          leave-from-class="transform translate-y-0 opacity-100"
          leave-to-class="transform -translate-y-2 opacity-0"
        >
          <div v-if="mobileMenuOpen" class="absolute top-full right-0 mt-4 w-48 bg-white border border-black/10 shadow-2xl p-4 flex flex-col space-y-3 items-end">
            <NuxtLink
              v-for="link in navLinks"
              :key="link.path"
              :to="link.path"
              @click="mobileMenuOpen = false"
              class="text-right hover:text-blue-600 transition-colors"
              active-class="font-bold text-blue-600"
            >
              {{ link.name }}
            </NuxtLink>
          </div>
        </Transition>
      </div>

    </div>
  </nav>

  <!-- Spacer to prevent content from going under fixed nav -->
  <div class="h-24 md:h-32" />
</template>

<script setup lang="ts">
import { ref, watch, onMounted, onUnmounted } from 'vue'
import { useConfig } from '~/composables/useConfig'
import { useRoute } from 'vue-router'

const { profile } = useConfig()
const mobileMenuOpen = ref(false)
const currentTime = ref('')
let timer: ReturnType<typeof setInterval> | null = null

const navLinks = [
  { name: 'Home', path: '/' },
  { name: 'Assignments', path: '/assignments' },
  { name: 'Portfolio', path: '/portfolio' },
  { name: 'Achievements', path: '/achievements' },
  { name: 'Skills', path: '/skills' },
  { name: 'Organizations', path: '/organizations' },
  { name: 'Profile', path: '/profile' },
  { name: 'Contact', path: '/contact' },
]

// Update time every minute
const updateTime = () => {
  const now = new Date()
  currentTime.value = now.toLocaleTimeString('en-US', { 
    hour12: false, 
    hour: '2-digit', 
    minute: '2-digit' 
  })
}

onMounted(() => {
  updateTime()
  timer = setInterval(updateTime, 60000)
})

onUnmounted(() => {
  if (timer) clearInterval(timer)
})

// Close mobile menu on route change
const route = useRoute()
watch(() => route.path, () => {
  mobileMenuOpen.value = false
})
</script>
