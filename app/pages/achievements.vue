<template>
  <div class="min-h-screen bg-transparent pt-32 pb-24 px-6 md:px-12 max-w-[1400px] mx-auto">
    <div v-if="achievements">
      <!-- Minimalist Header -->
      <div class="mb-24 flex flex-col md:flex-row md:items-end justify-between border-b border-black pb-8">
        <div>
          <h1 class="font-serif text-[3rem] md:text-[5rem] leading-none mb-4 text-black">Distinctions</h1>
          <p class="font-sans text-sm text-black/60 uppercase tracking-widest">Prix et Récompenses</p>
        </div>
        
        <div class="mt-8 md:mt-0 flex space-x-8 text-black/80 font-serif">
          <div>
            <span class="block text-4xl mb-1">{{ achievements.length }}</span>
            <span class="font-sans text-xs uppercase tracking-widest text-black/50">Total</span>
          </div>
          <div>
            <span class="block text-4xl mb-1">{{ achievements.filter(a => a.type === 'competition').length }}</span>
            <span class="font-sans text-xs uppercase tracking-widest text-black/50">Compétitions</span>
          </div>
        </div>
      </div>

      <!-- Brutalist List View -->
      <div class="flex flex-col border-t border-black">
        <div 
          v-for="achievement in achievements" 
          :key="achievement.title" 
          class="group border-b border-black py-8 md:py-12 transition-colors hover:bg-black/[0.02]"
        >
          <div class="grid grid-cols-1 md:grid-cols-12 gap-8 items-start">
            
            <!-- Type & Year -->
            <div class="md:col-span-2 font-sans text-xs uppercase tracking-widest text-black/50 flex flex-col md:block space-y-2 md:space-y-0 text-left">
              <span class="text-blue-600 font-medium md:block md:mb-2">{{ achievement.type }}</span>
              <span class="md:block">{{ achievement.year }}</span>
            </div>

            <!-- Title & Organization -->
            <div class="md:col-span-6 cursor-pointer">
              <h3 class="font-serif text-2xl md:text-4xl text-black mb-3 group-hover:text-blue-600 transition-colors">
                {{ achievement.title }}
              </h3>
              <p class="font-sans text-black/80 font-medium mb-4">
                {{ achievement.organization }}
              </p>
              <p class="font-sans text-black/60 max-w-xl leading-relaxed text-sm">
                {{ achievement.description }}
              </p>
            </div>

            <!-- Rank/Medal (Minimal) -->
            <div class="md:col-span-4 flex md:justify-end mt-4 md:mt-0">
              <span class="font-serif italic text-xl md:text-2xl text-black group-hover:text-blue-600 transition-colors">
                {{ achievement.rank }}
              </span>
            </div>

          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
const { achievements } = useConfig()

useHead({
  title: 'Achievements | Muhammad Faqih Shiam',
  meta: [{ name: 'description', content: 'My professional achievements and certifications' }]
})
</script>
