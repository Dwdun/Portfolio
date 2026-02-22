<template>
  <div class="min-h-screen bg-transparent pt-32 pb-24 px-6 md:px-12 max-w-[1400px] mx-auto">
    <div v-if="assignments">
      <!-- Minimalist Header -->
      <div class="mb-24 flex flex-col md:flex-row md:items-end justify-between border-b border-black pb-8">
        <div>
          <h1 class="font-serif text-[3rem] md:text-[5rem] leading-none mb-4 text-black">Assignments</h1>
          <p class="font-sans text-sm text-black/60 uppercase tracking-widest">Open Recruitment Assignments</p>
        </div>
        
        <div class="mt-8 md:mt-0 flex space-x-8 text-black/80 font-serif">
          <div>
            <span class="block text-4xl mb-1">{{ assignments.length }}</span>
            <span class="font-sans text-xs uppercase tracking-widest text-black/50">Total</span>
          </div>
        </div>
      </div>

      <!-- Brutalist List View -->
      <div class="flex flex-col border-t border-black">
        <NuxtLink 
          v-for="assignment in assignments" 
          :key="assignment.id" 
          :to="`/assignments/${assignment.id}`"
          class="group block border-b border-black py-8 md:py-12 transition-colors hover:bg-black/[0.02]"
        >
          <div class="grid grid-cols-1 md:grid-cols-12 gap-8 items-start">
            
            <!-- Target & Type -->
            <div class="md:col-span-2 font-sans text-xs uppercase tracking-widest text-black/50 flex flex-col md:block space-y-2 md:space-y-0 text-left">
              <span class="text-blue-600 font-medium md:block md:mb-2">No. {{ String(assignment.id).padStart(2, '0') }}</span>
              <span class="md:block">{{ assignment.type }}</span>
            </div>

            <!-- Title & Description -->
            <div class="md:col-span-6">
              <h3 class="font-serif text-2xl md:text-4xl text-black mb-3 group-hover:text-blue-600 transition-colors">
                {{ assignment.title }}
              </h3>
              <p class="font-sans text-black/60 max-w-xl leading-relaxed text-sm mb-4">
                {{ assignment.description }}
              </p>
            </div>

            <!-- Technologies (Tags) -->
            <div class="md:col-span-3">
              <div v-if="assignment.technologies" class="flex flex-wrap gap-2">
                <span v-for="tech in assignment.technologies" :key="tech" class="font-sans text-[0.65rem] uppercase tracking-widest border border-black/20 text-black/60 px-2 py-1">
                  {{ tech }}
                </span>
              </div>
            </div>

            <!-- View Arrow -->
            <div class="md:col-span-1 flex md:justify-end mt-4 md:mt-0 opacity-0 group-hover:opacity-100 transition-opacity">
               <span class="font-serif italic text-2xl text-blue-600">→</span>
            </div>

          </div>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
const { assignments } = useConfig()

useHead({
  title: 'Assignments | Muhammad Faqih Shiam',
  meta: [{ name: 'description', content: 'My assignments and coursework' }]
})
</script>
