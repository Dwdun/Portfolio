<template>
  <div class="min-h-screen bg-transparent pt-32 pb-24 px-6 md:px-12 max-w-[1400px] mx-auto">
    
    <div v-if="projects">
      <!-- Minimalist Header -->
      <div class="mb-24 flex flex-col md:flex-row md:items-end justify-between border-b border-black pb-8">
        <div>
          <h1 class="font-serif text-[3rem] md:text-[5rem] leading-none mb-4 text-black">Projets</h1>
          <p class="font-sans text-sm text-black/60 uppercase tracking-widest">Selected Works & Applications</p>
        </div>
        
        <div class="mt-8 md:mt-0 max-w-sm">
          <p class="font-serif text-lg text-black/80 italic">
            Specific details and performance metrics are protected under confidentiality agreements and are available for discussion under NDA.
          </p>
        </div>
      </div>

      <!-- Brutalist List View -->
      <div class="flex flex-col border-t border-black">
        <NuxtLink 
          v-for="(project, index) in projects" 
          :key="project.id" 
          :to="`/portfolio/${project.id}`"
          class="block group border-b border-black py-8 md:py-12 transition-colors hover:bg-black/[0.02]"
        >
          <div class="grid grid-cols-1 md:grid-cols-12 gap-8 items-start">
            
            <!-- Index & Category -->
            <div class="md:col-span-2 font-sans text-xs uppercase tracking-widest text-black/50">
              <span class="block mb-2">0{{ index + 1 }}</span>
              <span class="text-blue-600 font-medium">{{ project.category }}</span>
            </div>

            <!-- Title & Description -->
            <div class="md:col-span-6 cursor-pointer">
              <h3 class="font-serif text-3xl md:text-5xl text-black mb-4 group-hover:text-blue-600 transition-colors">
                {{ project.title }}
              </h3>
              <p class="font-sans text-black/70 mb-6 max-w-xl leading-relaxed">
                {{ project.description }}
              </p>
              
              <!-- Tech Stack Tags (Minimal) -->
              <div class="flex flex-wrap gap-3">
                <span v-for="tech in project.techStack" :key="tech" class="font-sans text-xs border border-black/20 px-3 py-1 rounded-full text-black/80">
                  {{ tech }}
                </span>
              </div>
            </div>

            <!-- Features & NDA -->
            <div class="md:col-span-4 max-w-sm">
              <ul class="space-y-2 mb-6 border-l border-black/10 pl-6">
                <li v-for="feature in project.features.slice(0,3)" :key="feature" class="font-sans text-sm text-black/60">
                  — {{ feature }}
                </li>
              </ul>

              <div v-if="project.nda" class="font-sans text-xs text-red-600/80 flex items-center border border-red-200 bg-red-50 px-3 py-2 rounded">
                <svg class="w-4 h-4 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
                </svg>
                Details under NDA
              </div>
            </div>

            <!-- Previews for Slain The Slime -->
            <div v-if="project.id === 4" class="col-span-12 mt-8">
              <div class="block group/gallery border-t border-black/10 pt-8">
                <div class="flex items-center justify-between mb-6">
                  <h4 class="font-sans text-xs uppercase tracking-widest text-black/50">Asset Previews</h4>
                  <span class="font-sans text-xs uppercase tracking-widest text-blue-600 opacity-0 group-hover/gallery:opacity-100 transition-opacity">View Full Details →</span>
                </div>
                <!-- Mini Gallery -->
                <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                  <div class="aspect-square bg-black/5 p-4 flex items-center justify-center border border-black/10 overflow-hidden">
                    <img src="/assets/slain-the-slime/boss-slime.gif" class="w-full h-full object-contain filter grayscale group-hover/gallery:grayscale-0 transition-all duration-500 scale-125" alt="Boss Slime" loading="lazy" />
                  </div>
                  <div class="aspect-square bg-black/5 p-4 flex items-center justify-center border border-black/10 overflow-hidden">
                    <img src="/assets/slain-the-slime/slime.gif" class="w-full h-full object-contain filter grayscale group-hover/gallery:grayscale-0 transition-all duration-500 scale-150" alt="Slime" loading="lazy" />
                  </div>
                  <div class="aspect-square bg-black/5 p-4 flex items-center justify-center border border-black/10 overflow-hidden hidden md:flex">
                    <img src="/assets/slain-the-slime/vfx_boss-slime.gif" class="w-full h-full object-contain filter grayscale group-hover/gallery:grayscale-0 transition-all duration-500 scale-125" alt="VFX" loading="lazy" />
                  </div>
                  <div class="aspect-square bg-black/5 p-4 flex items-center justify-center border border-black/10 overflow-hidden hidden md:flex relative">
                     <img src="/assets/slain-the-slime/slime_sheet.png" class="absolute h-full w-auto max-w-none object-cover opacity-50 filter grayscale group-hover/gallery:grayscale-0 transition-all duration-500" style="object-position: left center;" alt="Sprite Sheet" loading="lazy" />
                  </div>
                </div>
              </div>
            </div>

            <!-- Generic CTA / Arrow for Projects -->
            <div v-if="project.id !== 4" class="col-span-12 mt-8 border-t border-black/10 pt-6 flex justify-between md:justify-end opacity-0 group-hover:opacity-100 transition-opacity">
              <span class="font-sans text-xs uppercase tracking-widest text-black/30 md:hidden">Project Info</span>
              <span class="font-sans text-xs uppercase tracking-widest text-black/50 inline-flex items-center gap-2 text-blue-600">
                View Full Details <span class="group-hover:translate-x-1 transition-transform">→</span>
              </span>
            </div>

          </div>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { useConfig } from '~/composables/useConfig'

const { projects } = useConfig()

useHead({
  title: 'Portfolio | Muhammad Faqih Shiam',
  meta: [{ name: 'description', content: 'My recent projects and work' }]
})
</script>
