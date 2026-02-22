<template>
  <div class="min-h-screen bg-transparent pt-32 pb-24 px-6 md:px-12 max-w-[1400px] mx-auto">
    <div v-if="organizations">
      <!-- Minimalist Header -->
      <div class="mb-24 flex flex-col md:flex-row md:items-end justify-between border-b border-black pb-8">
        <div>
          <h1 class="font-serif text-[3rem] md:text-[5rem] leading-none mb-4 text-black">Organisations</h1>
          <p class="font-sans text-sm text-black/60 uppercase tracking-widest">Community & Leadership</p>
        </div>
      </div>

      <!-- Brutalist List View -->
      <div class="flex flex-col border-t border-black">
        <div 
          v-for="org in organizations" 
          :key="org.organization" 
          class="group border-b border-black py-8 md:py-12 transition-colors hover:bg-black/[0.02]"
        >
          <div class="grid grid-cols-1 md:grid-cols-12 gap-8 items-start">
            
            <!-- Target & Timeline -->
            <div class="md:col-span-3 font-sans text-xs uppercase tracking-widest text-black/50">
              <span v-if="org.current" class="text-blue-600 font-medium block mb-2">Actuel</span>
              <span class="block mb-1">{{ org.period }}</span>
              <span class="block">{{ org.location }}</span>
            </div>

            <!-- Title & Organization -->
            <div class="md:col-span-5 cursor-pointer">
              <h3 class="font-serif text-2xl md:text-3xl text-black mb-2 group-hover:text-blue-600 transition-colors">
                {{ org.title }}
              </h3>
              <p class="font-sans text-black/80 font-medium mb-6">
                {{ org.organization }}
              </p>
            </div>

            <!-- Responsibilities -->
            <div class="md:col-span-4">
              <ul class="space-y-2 border-l border-black/10 pl-6">
                <li v-for="(resp, idx) in org.responsibilities.slice(0,3)" :key="idx" class="font-sans text-sm text-black/60">
                  — {{ resp }}
                </li>
              </ul>
            </div>

          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
const { organizations } = useConfig()

useHead({
  title: 'Organizations | Muhammad Faqih Shiam',
  meta: [{ name: 'description', content: 'My organizational experience and leadership roles' }]
})
</script>
