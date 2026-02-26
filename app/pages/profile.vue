<template>
  <div class="min-h-screen bg-transparent pt-32 pb-24 px-6 md:px-12 max-w-[1400px] mx-auto">
    <div v-if="profile && education && languages && experience">
      
      <!-- Brutalist Header & Bio -->
      <div class="mb-24 flex flex-col md:flex-row md:items-start justify-between border-b border-black pb-16">
        <div class="md:w-1/3 mb-8 md:mb-0">
          <h1 class="font-serif text-[3rem] md:text-[5rem] leading-none text-black">Profile</h1>
          <p class="font-sans text-sm text-black/60 uppercase tracking-widest mt-4">About Me</p>
        </div>
        <div class="md:w-2/3 md:pl-16 flex flex-col lg:flex-row gap-12 items-center lg:items-start">
          <p class="font-serif text-2xl md:text-3xl text-black leading-relaxed flex-1">
            {{ profile.bio }}
          </p>
          <div class="w-full lg:w-auto flex justify-center perspective-[1200px] mt-8 lg:mt-0 transform scale-75 lg:scale-100 origin-top">
            <MobileScreen3D />
          </div>
        </div>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-12 gap-16 lg:gap-8">
        
        <!-- Left Column: Education & Languages -->
        <div class="lg:col-span-4 space-y-16">
          
          <!-- Education -->
          <section>
            <h2 class="font-sans text-xs uppercase tracking-widest text-black/50 mb-8 border-b border-black/20 pb-4">Education</h2>
            <div class="space-y-8 mt-8">
              <div v-for="edu in education" :key="edu.institution" class="group">
                <h3 class="font-serif text-xl sm:text-2xl text-black mb-1 group-hover:text-blue-600 transition-colors">{{ edu.degree }}</h3>
                <p class="font-sans text-black/80">{{ edu.institution }}</p>
                <div class="flex items-center space-x-2 font-sans text-xs text-black/50 mt-2">
                  <span>{{ edu.period }}</span>
                  <span>—</span>
                  <span>{{ edu.location }}</span>
                </div>
              </div>
            </div>
          </section>

          <!-- Languages -->
          <section>
            <h2 class="font-sans text-xs uppercase tracking-widest text-black/50 mb-8 border-b border-black/20 pb-4">Language Proficiency</h2>
            <div class="space-y-8 mt-8">
              <div v-for="lang in languages" :key="lang.language" class="group">
                <div class="flex justify-between items-baseline mb-1">
                  <h3 class="font-serif text-xl sm:text-2xl text-black group-hover:text-blue-600 transition-colors">{{ lang.language }}</h3>
                  <span class="font-serif text-xl text-black/40">{{ lang.percentage.toFixed(1) }}%</span>
                </div>
                <p class="font-sans text-black/80">{{ lang.level }}</p>
                <div class="flex items-center space-x-2 font-sans text-xs text-black/50 mt-2">
                  <span>{{ lang.certification }}</span>
                  <span v-if="lang.score">Score: {{ lang.score }}/{{ lang.maxScore }}</span>
                </div>
              </div>
            </div>
          </section>

        </div>

        <!-- Right Column: Professional Experience -->
        <div class="lg:col-span-8 lg:pl-12 lg:border-l border-black/20">
          <h2 class="font-sans text-xs uppercase tracking-widest text-black/50 mb-8 border-b border-black/20 pb-4">Professional Experience</h2>
          
          <div class="flex flex-col">
            <div v-for="exp in experience" :key="exp.title" class="group border-b border-black/10 py-8 last:border-0 hover:bg-black/[0.02] transition-colors -mx-6 px-6 sm:mx-0 sm:px-0 sm:hover:bg-transparent">
              <div class="grid grid-cols-1 md:grid-cols-12 gap-4 items-start mb-6">
                <!-- Meta -->
                <div class="md:col-span-3 font-sans text-xs uppercase tracking-widest text-black/50 flex flex-col space-y-1 pt-1">
                  <span class="text-blue-600">{{ exp.period }}</span>
                  <span>{{ exp.location }}</span>
                </div>
                <!-- Title & Company -->
                <div class="md:col-span-9">
                  <h3 class="font-serif text-2xl md:text-3xl text-black mb-2 group-hover:text-blue-600 transition-colors">{{ exp.title }}</h3>
                  <p class="font-sans text-black/80 font-medium">{{ exp.company }}</p>
                </div>
              </div>

              <div class="grid grid-cols-1 md:grid-cols-12 gap-4 items-start">
                <div class="md:col-span-3"></div>
                <div class="md:col-span-9">
                  <ul class="space-y-3 font-sans text-black/80 text-sm mb-6">
                    <li v-for="(resp, idx) in exp.responsibilities" :key="idx" class="flex items-start">
                      <span class="text-blue-600 mr-3 font-serif italic text-lg leading-none">/</span>
                      <span class="pt-1 leading-relaxed">{{ resp }}</span>
                    </li>
                  </ul>
                  
                  <div class="flex flex-wrap gap-2">
                    <span v-for="tech in exp.techStack" :key="tech" class="font-sans text-[0.65rem] uppercase tracking-widest border border-black/20 text-black/60 px-2 py-1">
                      {{ tech }}
                    </span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      
        <!-- Museum of Certificates -->
        <section class="mt-24 pt-16 border-t border-black">
          <h2 class="font-sans text-xs uppercase tracking-widest text-black/50 mb-12 text-center md:text-left">Museum of Certificates</h2>
          
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            <div 
              v-for="(cert, index) in certificates" 
              :key="index" 
              class="group cursor-pointer"
              @click="selectedCertificate = cert"
            >
              <div class="aspect-[4/3] bg-black/5 p-4 border border-black/10 flex items-center justify-center overflow-hidden hover:border-black/30 transition-colors">
                <img :src="cert.path" :alt="cert.name" class="max-w-full max-h-full object-contain group-hover:scale-105 transition-transform duration-500" loading="lazy" />
              </div>
              <p class="mt-4 font-sans text-xs uppercase tracking-widest text-black/60 text-center group-hover:text-blue-600 transition-colors">{{ cert.name }}</p>
            </div>
          </div>
        </section>

      </div> <!-- End v-if="profile &&..." -->

      <!-- Certificate Modal -->
      <Transition name="fade">
        <div v-if="selectedCertificate" class="fixed inset-0 z-[100] flex justify-center items-center p-4 backdrop-blur-sm bg-black/60" @click.self="selectedCertificate = null">
          <div class="relative max-w-5xl w-full max-h-[90vh] bg-white p-2 flex flex-col items-center">
            <button @click="selectedCertificate = null" class="absolute -top-12 right-0 text-white font-sans text-sm tracking-widest uppercase hover:opacity-70 transition-opacity">
              [ Close ]
            </button>
            <img :src="selectedCertificate.path" :alt="selectedCertificate.name" class="w-full h-auto max-h-[85vh] object-contain border border-black/10" />
            <p class="mt-4 font-sans text-sm tracking-widest uppercase text-black mb-2">{{ selectedCertificate.name }}</p>
          </div>
        </div>
      </Transition>
    </div> <!-- End min-h-screen -->
</template>

<script setup lang="ts">
import { ref } from 'vue'

const { profile, education, languages, experience } = useConfig()

const selectedCertificate = ref<{name: string, path: string} | null>(null)

const certificates = [
  { name: 'Certificate 1', path: '/assets/Sertifikat kompetensi/Cuplikan layar 2026-02-26 053614.png' },
  { name: 'Certificate 2', path: '/assets/Sertifikat kompetensi/Cuplikan layar 2026-02-26 053835.png' },
  { name: 'Certificate 3', path: '/assets/Sertifikat kompetensi/Cuplikan layar 2026-02-26 053854.png' },
  { name: 'Certificate 4', path: '/assets/Sertifikat kompetensi/Cuplikan layar 2026-02-26 053912.png' },
  { name: 'Certificate 5', path: '/assets/Sertifikat kompetensi/Cuplikan layar 2026-02-26 053934.png' },
  { name: 'Certificate 6', path: '/assets/Sertifikat kompetensi/Cuplikan layar 2026-02-26 054132.png' },
  { name: 'Certificate 7', path: '/assets/Sertifikat kompetensi/Cuplikan layar 2026-02-26 054143.png' },
  { name: 'Certificate 8', path: '/assets/Sertifikat kompetensi/IMG-20250213-WA0041.jpg' }
]

useHead({
  title: 'Profile | Muhammad Faqih Shiam',
  meta: [{ name: 'description', content: 'My professional journey and background' }]
})
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
