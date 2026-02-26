<template>
  <div 
    class="custom-cursor hidden md:block" 
    :style="{ transform: `translate3d(${x}px, ${y}px, 0)` }"
    :class="{ 'cursor-active': isActive }"
  >
    <div class="cursor-dot"></div>
    <div class="cursor-ring"></div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const x = ref(-100)
const y = ref(-100)
const isActive = ref(false)

const updateCursor = (e: MouseEvent) => {
  x.value = e.clientX
  y.value = e.clientY
  
  // Check if hovering over clickable elements
  const target = e.target as HTMLElement
  isActive.value = !!target.closest('a, button, input, [role="button"], .cursor-pointer')
}

onMounted(() => {
  window.addEventListener('mousemove', updateCursor)
})

onUnmounted(() => {
  window.removeEventListener('mousemove', updateCursor)
})
</script>

<style scoped>
.custom-cursor {
  position: fixed;
  top: 0;
  left: 0;
  pointer-events: none;
  z-index: 9999;
  mix-blend-mode: difference;
}

.cursor-dot {
  position: absolute;
  top: -2px;
  left: -2px;
  width: 4px;
  height: 4px;
  background-color: #3b82f6; /* blue-500 */
  border-radius: 50%;
  transition: transform 0.2s cubic-bezier(0.25, 1, 0.5, 1);
}

.cursor-ring {
  position: absolute;
  top: -12px;
  left: -12px;
  width: 24px;
  height: 24px;
  border: 1px solid #3b82f6; /* blue-500 */
  border-radius: 50%;
  transition: transform 0.3s cubic-bezier(0.25, 1, 0.5, 1), background-color 0.3s, border-color 0.3s;
}

/* Active state (hovering over links/buttons) */
.cursor-active .cursor-dot {
  transform: scale(0);
}

.cursor-active .cursor-ring {
  transform: scale(1.5);
  background-color: rgba(37, 99, 235, 0.2); /* blue-600 with opacity */
  border-color: rgba(37, 99, 235, 0.8);
}
</style>
