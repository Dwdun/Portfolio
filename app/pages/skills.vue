<template>
  <div class="min-h-screen bg-transparent pt-32 pb-24 px-6 md:px-12 max-w-[1400px] mx-auto">
    <div v-if="skills">
      <!-- Minimalist Header -->
      <div class="mb-24 flex flex-col md:flex-row md:items-end justify-between border-b border-black pb-8">
        <div>
          <h1 class="font-serif text-[3rem] md:text-[5rem] leading-none mb-4 text-black">Compétences</h1>
          <p class="font-sans text-sm text-black/60 uppercase tracking-widest">Technologies & Pratiques</p>
        </div>
      </div>

      <div class="space-y-24">
        <!-- Languages -->
        <section class="border-t border-black pt-8">
          <div class="grid grid-cols-1 md:grid-cols-12 gap-8">
            <div class="md:col-span-3">
              <h2 class="font-sans text-xs uppercase tracking-widest text-black/50">01. Languages</h2>
            </div>
            <div class="md:col-span-9 flex flex-wrap gap-4">
              <span 
                v-for="lang in skills.languages" 
                :key="lang.name"
                class="font-mono text-sm md:text-base border border-black/20 text-black px-4 py-2 hover:bg-black hover:text-white transition-colors cursor-default"
              >
                {{ lang.name }}
              </span>
            </div>
          </div>
        </section>

        <!-- Frameworks & Tools -->
        <section class="border-t border-black pt-8">
          <div class="grid grid-cols-1 md:grid-cols-12 gap-8">
            <div class="md:col-span-3">
              <h2 class="font-sans text-xs uppercase tracking-widest text-black/50">02. Frameworks & Outils</h2>
            </div>
            <div class="md:col-span-9 flex flex-wrap gap-4">
              <span 
                v-for="framework in skills.frameworks" 
                :key="framework.name"
                class="font-mono text-sm md:text-base border border-black/20 text-black px-4 py-2 hover:bg-black hover:text-white transition-colors cursor-default"
              >
                {{ framework.name }}
              </span>
            </div>
          </div>
        </section>

        <!-- Concepts & Practices -->
        <section class="border-t border-black pt-8">
          <div class="grid grid-cols-1 md:grid-cols-12 gap-8">
            <div class="md:col-span-3">
              <h2 class="font-sans text-xs uppercase tracking-widest text-black/50">03. Concepts & Pratiques</h2>
            </div>
            <div class="md:col-span-9 flex flex-wrap gap-4">
              <span 
                v-for="concept in skills.concepts" 
                :key="concept.name"
                class="font-mono text-sm md:text-base border border-black/20 text-black px-4 py-2 hover:bg-black hover:text-white transition-colors cursor-default"
              >
                {{ concept.name }}
              </span>
            </div>
          </div>
        </section>
      </div>

    </div>
  </div>
</template>

<script setup lang="ts">
import { useScrollAnimations } from '~/composables/useScrollAnimations'

const { skills } = useConfig()
useScrollAnimations()

useHead({
  title: 'Tech Stack | Muhammad Faqih Shiam',
  meta: [{ name: 'description', content: 'My technical skills and proficiency levels' }]
})
</script>
