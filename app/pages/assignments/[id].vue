<template>
  <div class="min-h-screen bg-transparent pt-32 pb-24 px-6 md:px-12 max-w-[1400px] mx-auto">
    
    <div v-if="assignment">
      <!-- Minimalist Back Button -->
      <NuxtLink to="/assignments" class="inline-block font-sans text-sm uppercase tracking-widest text-black hover:opacity-50 transition-opacity border-b border-black pb-1 mb-16">
        ← Back to assignments
      </NuxtLink>

      <!-- Brutalist Header -->
      <div class="mb-16 md:mb-24">
        <!-- Meta Row -->
        <div class="flex items-center space-x-4 font-sans text-xs uppercase tracking-widest text-black/50 mb-6">
          <span class="text-blue-600 font-medium">No. {{ String(assignment.id).padStart(2, '0') }}</span>
          <span>—</span>
          <span>{{ assignment.type }}</span>
        </div>
        
        <h1 class="font-serif text-[3rem] md:text-[5rem] lg:text-[6rem] leading-[1.1] tracking-tight text-black mb-6 max-w-5xl">
          {{ assignment.title }}
        </h1>
        
        <p class="font-sans text-lg md:text-xl text-black/80 max-w-3xl leading-relaxed">
          {{ assignment.description }}
        </p>
      </div>

      <!-- Detail Grid Layout -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-16 lg:gap-8 border-t border-black pt-16">
        
        <!-- Left Col: Details & Meta -->
        <div class="lg:col-span-4 space-y-16">
          
          <!-- Technologies -->
          <div v-if="assignment.technologies">
            <h2 class="font-sans text-xs uppercase tracking-widest text-black/50 mb-6">Technologies</h2>
            <div class="flex flex-wrap gap-2">
              <span v-for="tech in assignment.technologies" :key="tech" class="font-mono text-sm border border-black/20 text-black px-3 py-1 cursor-default">
                {{ tech }}
              </span>
            </div>
          </div>

          <!-- Links -->
          <div v-if="assignment.liveUrl || assignment.githubUrl">
            <h2 class="font-sans text-xs uppercase tracking-widest text-black/50 mb-6">Links / Access</h2>
            <div class="flex flex-col space-y-4">
              <a v-if="assignment.liveUrl" :href="assignment.liveUrl" target="_blank" class="w-fit font-sans text-lg text-black hover:text-blue-600 border-b border-black/20 pb-1 transition-colors">
                Live Demo ↗
              </a>
              <a v-if="assignment.githubUrl" :href="assignment.githubUrl" target="_blank" class="w-fit font-sans text-lg text-black hover:text-blue-600 border-b border-black/20 pb-1 transition-colors">
                Source Code ↗
              </a>
            </div>
          </div>
          
        </div>

        <!-- Right Col: Objectives, Results & Files -->
        <div class="lg:col-span-8 space-y-16 lg:pl-12 lg:border-l border-black/20">
          
          <!-- Objectives -->
          <div v-if="assignment.objectives?.length">
            <h2 class="font-serif text-3xl mb-8 text-black">Objectives</h2>
            <ul class="space-y-4 font-sans text-black/80">
              <li v-for="(obj, idx) in assignment.objectives" :key="idx" class="flex items-start">
                <span class="text-blue-600 mr-4 font-serif italic text-xl">/</span>
                <span class="pt-1">{{ obj }}</span>
              </li>
            </ul>
          </div>

          <!-- Results -->
          <div v-if="assignment.results?.length">
            <h2 class="font-serif text-3xl mb-8 text-black">Results</h2>
            <ul class="space-y-4 font-sans text-black/80">
              <li v-for="(result, idx) in assignment.results" :key="idx" class="flex items-start">
                <span class="text-blue-600 mr-4 font-serif italic text-xl">/</span>
                <span class="pt-1">{{ result }}</span>
              </li>
            </ul>
          </div>

          <!-- File / Media Block -->
          <div v-if="assignment.file" class="pt-8 border-t border-black/10">
            <h2 class="font-serif text-3xl mb-8 text-black">Attached Media</h2>
            
            <div v-if="assignment.type === 'pdf'" class="space-y-8 flex flex-col items-center border border-black/20 p-8 hover:bg-black/[0.02] transition-colors">
              <p class="font-sans text-black/60">A PDF document is associated with this assignment.</p>
              
              <!-- PDF Preview Feature -->
              <div class="w-full h-[500px] md:h-[700px] border border-black/10 overflow-hidden shadow-sm bg-white">
                 <embed :src="assignment.file" type="application/pdf" class="w-full h-full" toolbar="0" view="FitH" />
              </div>

              <a :href="assignment.file" download target="_blank" rel="noopener noreferrer" class="inline-block bg-black text-white font-sans uppercase tracking-widest text-xs px-8 py-4 hover:bg-blue-600 transition-colors">
                Download Document ↓
              </a>
            </div>

            <div v-if="assignment.type === 'image'" class="space-y-6">
              <div class="border border-black/10 bg-black/[0.02] p-4">
                <img :src="assignment.file" :alt="assignment.title" class="w-full h-auto mix-blend-multiply" />
              </div>
              <a :href="assignment.file" download target="_blank" rel="noopener noreferrer" class="inline-block font-sans text-sm tracking-wider text-black border-b border-black hover:text-blue-600 hover:border-blue-600 transition-colors pb-1">
                Download Image ↓
              </a>
            </div>

            <div v-if="assignment.type === 'video'" class="space-y-6">
              <div class="border border-black/10 bg-black/[0.02] p-4">
                <video controls class="w-full">
                  <source :src="assignment.file" type="video/mp4" />
                  Your browser does not support the video tag.
                </video>
              </div>
              <a :href="assignment.file" download target="_blank" rel="noopener noreferrer" class="inline-block font-sans text-sm tracking-wider text-black border-b border-black hover:text-blue-600 hover:border-blue-600 transition-colors pb-1">
                Download Video ↓
              </a>
            </div>
            
          </div>

        </div>
      </div>
      
    </div>

    <!-- 404 State -->
    <div v-else class="flex flex-col items-center justify-center pt-32 text-center">
      <h1 class="font-serif text-[4rem] md:text-[6rem] leading-none text-black mb-8 italic">404 Error</h1>
      <p class="font-sans text-lg text-black/60 mb-12">The requested assignment does not exist or has been removed.</p>
      <NuxtLink to="/assignments" class="inline-block bg-black text-white font-sans uppercase tracking-widest text-xs px-8 py-4 hover:bg-blue-600 transition-colors">
        ← Back to assignments
      </NuxtLink>
    </div>

  </div>
</template>

<script setup lang="ts">
const route = useRoute()
const { assignments } = useConfig()

const assignment = computed(() => {
  const id = parseInt(route.params.id as string)
  return assignments.value?.find(a => a.id === id)
})

useHead({
  title: () => assignment.value ? `${assignment.value.title} | Muhammad Faqih Shiam` : 'Assignment Not Found',
  meta: [
    { name: 'description', content: () => assignment.value?.description || 'Assignment details' }
  ]
})
</script>
