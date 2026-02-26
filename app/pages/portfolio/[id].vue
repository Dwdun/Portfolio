<template>
  <div class="min-h-screen bg-transparent pt-32 pb-24 px-6 md:px-12 max-w-[1400px] mx-auto">
    <div v-if="project" :key="project.id">
      
      <!-- Brutalist Header -->
      <div class="mb-16 flex flex-col justify-between border-b border-black pb-16">
        <NuxtLink to="/portfolio" class="font-sans text-xs uppercase tracking-widest text-black/50 hover:text-blue-600 transition-colors mb-12 inline-flex items-center gap-2">
          ← Back to Portfolio
        </NuxtLink>
        
        <div class="flex flex-col md:flex-row md:items-end justify-between gap-8">
          <div class="md:w-2/3">
            <h1 class="font-serif text-[3rem] md:text-[5rem] lg:text-[6rem] leading-none text-black tracking-tight mb-6">
              {{ project.title }}
            </h1>
            <p class="font-sans text-lg md:text-xl text-black/80 max-w-2xl leading-relaxed">
              {{ project.description }}
            </p>
          </div>
          
          <div class="md:w-1/3 flex flex-col space-y-4 md:text-right">
            <div>
              <p class="font-sans text-xs uppercase tracking-widest text-black/50 mb-1">Role</p>
              <p class="font-sans text-base text-black/90">Lead Designer, Asset Creator</p>
            </div>
            <div>
              <p class="font-sans text-xs uppercase tracking-widest text-black/50 mb-1">Category</p>
              <p class="font-sans text-base text-blue-600">{{ project.category }}</p>
            </div>
            <div>
              <p class="font-sans text-xs uppercase tracking-widest text-black/50 mb-1">Tech Stack</p>
              <div class="flex flex-wrap gap-2 md:justify-end">
                <span v-for="tech in project.techStack" :key="tech" class="font-sans text-xs border border-black/20 px-3 py-1 rounded-full text-black/80">
                  {{ tech }}
                </span>
              </div>
            </div>
            <div v-if="project.link" class="pt-4">
              <a :href="project.link" target="_blank" rel="noopener noreferrer" class="font-sans text-xs uppercase tracking-widest text-black/50 hover:text-blue-600 transition-colors inline-flex items-center gap-1">
                {{ project.link.includes('itch.io') ? 'See the Game' : 'View Project' }} ↗
              </a>
            </div>
          </div>
        </div>
      </div>

      <!-- Slain the Slime Specific Gallery -->
      <div v-if="project.id === 4" class="space-y-24">
        
        <!-- Animations Section -->
        <section>
          <div class="grid grid-cols-1 md:grid-cols-12 gap-8 items-start mb-12">
            <div class="md:col-span-3">
              <h2 class="font-serif text-3xl md:text-4xl text-black">Animations</h2>
              <p class="font-sans text-sm text-black/60 mt-4 leading-relaxed">
                Smooth pixel art animations crafted frame-by-frame for dynamic combat feel and lively character movement.
              </p>
            </div>
            
            <div class="md:col-span-9 grid grid-cols-1 sm:grid-cols-2 gap-8">
              <!-- Boss Slime -->
              <div class="bg-[#f8f9fa] border border-black/10 p-12 flex flex-col justify-center items-center group relative overflow-hidden">
                <div class="absolute inset-0 bg-black/5 opacity-0 group-hover:opacity-100 transition-opacity"></div>
                <!-- Checkerboard background for transparency -->
                <div class="w-full aspect-square max-w-[300px] flex items-center justify-center" style="background-image: linear-gradient(45deg, #ccc 25%, transparent 25%), linear-gradient(-45deg, #ccc 25%, transparent 25%), linear-gradient(45deg, transparent 75%, #ccc 75%), linear-gradient(-45deg, transparent 75%, #ccc 75%); background-size: 20px 20px; background-position: 0 0, 0 10px, 10px -10px, -10px 0px;">
                  <img src="/assets/slain-the-slime/boss-slime.gif" alt="Boss Slime Animation" class="w-full h-auto max-h-full object-contain drop-shadow-2xl scale-125 md:scale-150" />
                </div>
                <div class="w-full border-t border-black/10 pt-4 mt-8 flex justify-between items-center z-10">
                  <span class="font-sans text-xs uppercase tracking-widest font-bold">Boss Slime</span>
                  <span class="font-sans text-[0.65rem] text-black/50 uppercase">Idle / Move</span>
                </div>
              </div>

              <!-- Normal Slime -->
              <div class="bg-[#f8f9fa] border border-black/10 p-12 flex flex-col justify-center items-center group relative overflow-hidden">
                <div class="absolute inset-0 bg-black/5 opacity-0 group-hover:opacity-100 transition-opacity"></div>
                <div class="w-full aspect-square max-w-[300px] flex items-center justify-center" style="background-image: linear-gradient(45deg, #ccc 25%, transparent 25%), linear-gradient(-45deg, #ccc 25%, transparent 25%), linear-gradient(45deg, transparent 75%, #ccc 75%), linear-gradient(-45deg, transparent 75%, #ccc 75%); background-size: 20px 20px; background-position: 0 0, 0 10px, 10px -10px, -10px 0px;">
                  <img src="/assets/slain-the-slime/slime.gif" alt="Normal Slime Animation" class="w-full h-auto max-h-full object-contain drop-shadow-2xl scale-150 md:scale-[2]" />
                </div>
                <div class="w-full border-t border-black/10 pt-4 mt-8 flex justify-between items-center z-10">
                  <span class="font-sans text-xs uppercase tracking-widest font-bold">Base Slime</span>
                  <span class="font-sans text-[0.65rem] text-black/50 uppercase">Mob Enemy</span>
                </div>
              </div>
            </div>
          </div>
        </section>

        <!-- VFX Section -->
        <section class="border-t border-black/10 pt-24">
          <div class="grid grid-cols-1 md:grid-cols-12 gap-8 items-start mb-12">
            <div class="md:col-span-3">
              <h2 class="font-serif text-3xl md:text-4xl text-black">VFX Assets</h2>
              <p class="font-sans text-sm text-black/60 mt-4 leading-relaxed">
                Hand-drawn visual effects designed to add impact to abilities and enemy interactions.
              </p>
            </div>
            
            <div class="md:col-span-9">
              <div class="bg-black border border-black p-12 flex flex-col justify-center items-center group relative w-full overflow-hidden min-h-[400px]">
                <img src="/assets/slain-the-slime/vfx_boss-slime.gif" alt="Boss Slime VFX" class="w-full max-w-[500px] h-auto object-contain scale-110" />
                <div class="absolute bottom-6 left-6 right-6 border-t border-white/20 pt-4 flex justify-between items-center text-white">
                  <span class="font-sans text-xs uppercase tracking-widest font-bold">Boss Impact VFX</span>
                  <span class="font-sans text-[0.65rem] text-white/50 uppercase">Animated</span>
                </div>
              </div>
              <div class="mt-4 flex justify-end">
                <a href="/assets/slain-the-slime/vfx_boss-slime.png" target="_blank" class="font-sans text-xs uppercase tracking-widest text-black/50 hover:text-blue-600 transition-colors">
                  View Source Image →
                </a>
              </div>
            </div>
          </div>
        </section>

        <!-- Sprite Sheets Section -->
        <section class="border-t border-black/10 pt-24 mb-24">
          <div class="grid grid-cols-1 md:grid-cols-12 gap-8 mb-12">
            <div class="md:col-span-3">
              <h2 class="font-serif text-3xl md:text-4xl text-black">Sprite Sheets</h2>
              <p class="font-sans text-sm text-black/60 mt-4 leading-relaxed">
                Optimized frame layouts formatted for easy engine integration, packing every animation into minimal memory space.
              </p>
            </div>
            
            <div class="md:col-span-9 space-y-12">
              
              <div class="group">
                <div class="flex justify-between items-end mb-4">
                  <h3 class="font-sans text-sm uppercase tracking-widest font-bold text-black">Boss Slime Sheet</h3>
                </div>
                <!-- Scrollable container for long sprite sheet -->
                <div class="w-full overflow-x-auto bg-[#f8f9fa] border border-black/10 flex items-center p-8 custom-scrollbar">
                  <img src="/assets/slain-the-slime/boss-slime_sheet.png" alt="Boss Slime Sprite Sheet" class="h-32 object-contain image-rendering-pixelated" />
                </div>
              </div>

              <div class="group">
                <div class="flex justify-between items-end mb-4">
                  <h3 class="font-sans text-sm uppercase tracking-widest font-bold text-black">Base Slime Sheet</h3>
                </div>
                <!-- Scrollable container for long sprite sheet -->
                <div class="w-full overflow-x-auto bg-[#f8f9fa] border border-black/10 flex items-center p-8 custom-scrollbar">
                  <img src="/assets/slain-the-slime/slime_sheet.png" alt="Base Slime Sprite Sheet" class="h-24 object-contain image-rendering-pixelated" />
                </div>
              </div>

            </div>
          </div>
        </section>

      </div>
      
      <!-- Generic Project Showcase (for non-Slain the Slime) -->
      <div v-else class="space-y-24">
        
        <section v-if="project.image" class="border-t border-black/10 pt-16">
          <div class="w-full bg-black/5 p-8 md:p-16 border border-black/10 flex items-center justify-center min-h-[50vh]">
            <img :src="project.image" :alt="project.title" class="max-w-full h-auto object-contain max-h-[70vh] drop-shadow-2xl" loading="lazy" />
          </div>
        </section>
        
        <section v-if="project.features && project.features.length > 0" class="border-t border-black/10 pt-16 mb-24">
          <div class="grid grid-cols-1 md:grid-cols-12 gap-8 items-start">
             <div class="md:col-span-4">
               <h2 class="font-serif text-3xl md:text-4xl text-black">Key Features & Deliverables</h2>
             </div>
             <div class="md:col-span-8">
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-8">
                  <div v-for="(feature, idx) in project.features" :key="idx" class="border-t-2 border-black pt-6">
                    <span class="font-sans text-xs uppercase tracking-widest text-black/50 block mb-2">0{{ idx + 1 }}</span>
                    <h3 class="font-sans text-lg font-bold text-black">{{ feature }}</h3>
                  </div>
                </div>
             </div>
          </div>
        </section>
        
      </div>
      
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import { useRoute } from 'vue-router'
import { useConfig } from '~/composables/useConfig'

definePageMeta({
  key: route => route.fullPath
})

const route = useRoute()
const { projects } = useConfig()

// Use a computed property that actively watches route.params.id
const project = computed(() => {
  if (!projects.value) return null
  const idValue = route.params.id
  const id = Array.isArray(idValue) ? Number(idValue[0]) : Number(idValue)
  return projects.value.find(p => p.id === id) || null
})

useHead({
  title: computed(() => project.value ? `${project.value.title} | Portfolio` : 'Project | Portfolio'),
  meta: [{ name: 'description', content: computed(() => project.value?.description || 'Project Details') }]
})
</script>

<style scoped>
.image-rendering-pixelated {
  image-rendering: pixelated; /* Crisp edges for pixel art */
}

.custom-scrollbar::-webkit-scrollbar {
  height: 8px;
}
.custom-scrollbar::-webkit-scrollbar-track {
  background: rgba(0,0,0,0.05);
}
.custom-scrollbar::-webkit-scrollbar-thumb {
  background: rgba(0,0,0,0.2);
  border-radius: 10px;
}
.custom-scrollbar::-webkit-scrollbar-thumb:hover {
  background: rgba(0,0,0,0.4);
}
</style>
