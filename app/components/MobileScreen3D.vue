<template>
  <div class="mobile-container w-full h-full flex justify-center items-center"
       @mousemove="handleMouseMove" 
       @mouseleave="handleMouseLeave">
    
    <div class="scene">
      <div class="phone" :style="phoneTransform">
        
        <!-- Phone Frame/Body Layers -->
        <div class="phone-face phone-back"></div>
        <div class="phone-face phone-front">
          <!-- The Screen -->
          <div class="screen relative overflow-hidden bg-yellow-400">
            <!-- Image inside the screen -->
            <img 
              src="/assets/gambar/faqih.jpeg" 
              alt="Faqih" 
              class="w-full h-full object-cover select-none mix-blend-multiply opacity-90"
              draggable="false"
            />
            
            <!-- Screen glare/reflection effect -->
            <div class="absolute inset-0 pointer-events-none glare" :style="glareStyle"></div>
          </div>
        </div>
        
        <!-- Edges -->
        <div class="phone-face phone-top"></div>
        <div class="phone-face phone-bottom"></div>
        <div class="phone-face phone-left"></div>
        <div class="phone-face phone-right"></div>
        
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

const rotateX = ref(15) // Slight starting tilt
const rotateY = ref(-15)
const glareX = ref(50)
const glareY = ref(50)

// Configurable sizes
const phoneWidth = 300
const phoneHeight = 600
const phoneDepth = 20

const handleMouseMove = (e: MouseEvent) => {
  const el = e.currentTarget as HTMLElement
  if (!el) return
  
  const rect = el.getBoundingClientRect()
  const x = e.clientX - rect.left
  const y = e.clientY - rect.top
  
  // Calculate relative position (-1 to 1)
  const xPct = (x / rect.width) * 2 - 1
  const yPct = (y / rect.height) * 2 - 1
  
  // Limit rotation angles for a realistic feel
  rotateY.value = xPct * 25 
  rotateX.value = -yPct * 25
  
  // Adjust glare position based on mouse
  glareX.value = (x / rect.width) * 100
  glareY.value = (y / rect.height) * 100
}

const handleMouseLeave = () => {
  // Reset back to idle position
  rotateX.value = 15
  rotateY.value = -15
  glareX.value = 50
  glareY.value = 50
}

const phoneTransform = computed(() => {
  return `transform: rotateX(${rotateX.value}deg) rotateY(${rotateY.value}deg);`
})

const glareStyle = computed(() => {
  return `background: radial-gradient(circle at ${glareX.value}% ${glareY.value}%, rgba(255,255,255,0.4) 0%, rgba(255,255,255,0) 60%);`
})
</script>

<style scoped>
.mobile-container {
  perspective: 1200px;
}

.scene {
  width: 300px;
  height: 600px;
  position: relative;
}

.phone {
  width: 100%;
  height: 100%;
  position: absolute;
  transform-style: preserve-3d;
  transition: transform 0.1s ease-out;
  cursor: grab;
}

.phone:active {
  cursor: grabbing;
}

.phone-face {
  position: absolute;
  background-color: #e5e7eb; /* Metallic gray chassis / light mode feel */
  border: 1px solid #d1d5db; /* Slight edge lines */
  box-shadow: inset 0 0 10px rgba(0,0,0,0.1);
  border-radius: 36px;
}

/* Back Face */
.phone-back {
  width: 300px;
  height: 600px;
  transform: translateZ(-10px) rotateY(180deg);
  background: linear-gradient(135deg, #f3f4f6 0%, #d1d5db 100%);
}

/* Front Face */
.phone-front {
  width: 300px;
  height: 600px;
  transform: translateZ(10px);
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #1a1a1a; /* Black bezels */
  padding: 12px; /* Bezel size */
}

.screen {
  width: 100%;
  height: 100%;
  border-radius: 26px; /* Inner screen border radius */
  position: relative;
  box-shadow: inset 0 0 4px rgba(0,0,0,0.5); /* Screen depth */
  overflow: hidden;
}

.glare {
  transition: background 0.1s ease-out;
  mix-blend-mode: screen;
}

/* Edges */
/* To make it pure CSS 3D rounded corners is hard on edges, 
   we will represent edges as boxes. The chassis will look a bit geometric but neat and brutalist. */

.phone-top, .phone-bottom {
  width: 250px; /* narrowed because of border radius trickery */
  height: 20px;
  left: 25px;
}
.phone-top {
  top: 0;
  transform: rotateX(90deg) translateZ(10px) translateY(-10px);
  transform-origin: top;
  border-radius: 0; /* Boxy edge */
}
.phone-bottom {
  bottom: 0;
  transform: rotateX(-90deg) translateZ(10px) translateY(10px);
  transform-origin: bottom;
  border-radius: 0;
}

.phone-left, .phone-right {
  width: 20px;
  height: 550px;
  top: 25px;
}
.phone-left {
  left: 0;
  transform: rotateY(-90deg) translateZ(10px) translateX(-10px);
  transform-origin: left;
  border-radius: 0;
}
.phone-right {
  right: 0;
  transform: rotateY(90deg) translateZ(10px) translateX(10px);
  transform-origin: right;
  border-radius: 0;
}
</style>
