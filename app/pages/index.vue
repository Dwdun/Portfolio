<template>
  <div class="min-h-screen bg-transparent overflow-x-hidden pt-12 md:pt-24">
    <!-- Hero Editorial Section -->
    <section class="max-w-[1400px] mx-auto px-6 sm:px-12 pb-16 md:pb-24 flex flex-col items-center justify-center text-center">
      
      <div v-if="profile" class="w-full relative z-10 flex flex-col items-center justify-center min-h-[60vh] md:min-h-[80vh] py-16 bg-white overflow-hidden" :style="{ '--mouse-x': mouseX + 'px', '--mouse-y': mouseY + 'px' }">
        
        <!-- Text and 3D Phone Container -->
        <div class="relative w-full max-w-5xl mx-auto mb-16 z-20 flex justify-center items-center">
          <!-- 3D Mobile Scene (Background exactly behind text) -->
          <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[100vw] h-[700px] md:h-[900px] flex justify-center items-center pointer-events-none" style="z-index: -1">
            <ClientOnly>
              <Mobile3D @move="handle3DMove" :scale="0.65" />
            </ClientOnly>
          </div>

          <!-- Main Typographic Intro, split for per-word hover -->
          <h1 class="relative font-serif text-[2.5rem] sm:text-[4rem] md:text-[5rem] lg:text-[6rem] leading-[1.1] tracking-tight text-black cursor-default text-center">
            <span class="hover-metallic">Hi</span> <span class="hover-metallic">there,</span> <span class="hover-metallic">I'm</span> <span class="hover-metallic italic font-medium text-blue-600">{{ profile.name }}</span><span class="hover-metallic">.</span> <span class="hover-metallic">I'm</span> <span class="hover-metallic">a</span> <span class="hover-metallic">student</span> <span class="hover-metallic">based</span> <span class="hover-metallic">in</span> <span class="hover-metallic">Bandung</span> <span class="hover-metallic">who</span> <span class="hover-metallic">loves</span> <span class="hover-metallic">bringing</span> <span class="hover-metallic">ideas</span> <span class="hover-metallic">to</span> <span class="hover-metallic">life</span> <span class="hover-metallic">through</span> <span class="hover-metallic italic font-medium">digital</span> <span class="hover-metallic italic font-medium">art</span><span class="hover-metallic">,</span> <span class="hover-metallic text-blue-600 font-medium">character</span> <span class="hover-metallic text-blue-600 font-medium">illustrations</span><span class="hover-metallic">,</span> <span class="hover-metallic">and</span> <span class="hover-metallic italic font-medium">game</span> <span class="hover-metallic italic font-medium">assets</span><span class="hover-metallic">.</span> <span class="hover-metallic">Welcome</span> <span class="hover-metallic">to</span> <span class="hover-metallic">my</span> <span class="hover-metallic">creative</span> <span class="hover-metallic">website.</span>
          </h1>
        </div>

        <!-- Read More Button -->
        <NuxtLink to="/portfolio" class="relative font-sans text-sm uppercase tracking-widest text-black hover:opacity-50 transition-opacity border-b border-black pb-1 mb-24 inline-block z-20">
          Read more →
        </NuxtLink>

        <!-- 3D Carousel Scene (Central Visual) -->
        <div class="scene w-full h-[300px] md:h-[500px] flex justify-center items-center mb-16 md:mb-32 perspective-[1000px] z-20">
          <div class="a3d hover:scale-105 transition-transform duration-700" style="--n: 6">
            <img class="card-3d shadow-2xl border border-black/10" src="/assets/gambar/Cyrene.jpg" style="--i: 0" alt="Cyrene illustration"/>
            <img class="card-3d shadow-2xl border border-black/10" src="/assets/gambar/HCW_Poster.png" style="--i: 1" alt="HCW Poster"/>
            <img class="card-3d shadow-2xl border border-black/10" src="/assets/gambar/jacq_update_2.png" style="--i: 2" alt="Jacq character artwork"/>
            <img class="card-3d shadow-2xl border border-black/10" src="/assets/gambar/kakavasha_final.png" style="--i: 3" alt="Kakavasha character art"/>
            <img class="card-3d shadow-2xl border border-black/10" src="/assets/gambar/phainon_final.png" style="--i: 4" alt="Phainon character art"/>
            <img class="card-3d shadow-2xl border border-black/10" src="/assets/gambar/sparxie_final.png" style="--i: 5" alt="Sparxie character art"/>
          </div>
        </div>
      </div>
    </section>

    <!-- Recent Minimal List -->
    <section v-if="achievements && projects" class="border-t border-black/20">
      <div class="max-w-[1400px] mx-auto grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3">
        
        <!-- Column 1: Projects -->
        <div class="border-b md:border-b-0 md:border-r border-black/20 p-6 md:p-12">
          <h2 class="uppercase tracking-widest text-xs mb-8 text-black/50">Recent Projects</h2>
          <div class="space-y-6">
            <div v-for="project in projects.slice(0,3)" :key="project.title" class="group">
              <NuxtLink to="/portfolio" class="block pb-6 mb-6 border-b border-black/10 last:border-0 last:pb-0 last:mb-0 hover:border-black/30 transition-colors">
                <h3 class="font-serif text-xl sm:text-2xl text-black leading-snug mb-2 group-hover:text-blue-600 transition-colors">{{ project.title }}</h3>
                <p class="font-sans text-xs text-black/60">{{ project.category }}</p>
              </NuxtLink>
            </div>
          </div>
          <NuxtLink to="/portfolio" class="inline-block mt-8 font-sans text-sm tracking-wider text-black border-b border-black hover:opacity-50 transition-opacity">
            View more →
          </NuxtLink>
        </div>

        <!-- Column 2: Experience / Achievements -->
        <div class="border-b md:border-b-0 lg:border-r border-black/20 p-6 md:p-12">
          <h2 class="uppercase tracking-widest text-xs mb-8 text-black/50">Experience & Achievements</h2>
          <div class="space-y-6">
            <div v-for="achievement in achievements.slice(0,3)" :key="achievement.title" class="group">
              <NuxtLink to="/achievements" class="block pb-6 mb-6 border-b border-black/10 last:border-0 last:pb-0 last:mb-0 hover:border-black/30 transition-colors">
                <h3 class="font-serif text-xl sm:text-2xl text-black leading-snug mb-2 group-hover:text-blue-600 transition-colors">{{ achievement.title }}</h3>
                <p class="font-sans text-xs text-black/60">{{ achievement.organization }}</p>
              </NuxtLink>
            </div>
          </div>
          <NuxtLink to="/achievements" class="inline-block mt-8 font-sans text-sm tracking-wider text-black border-b border-black hover:opacity-50 transition-opacity">
            View more →
          </NuxtLink>
        </div>

        <!-- Column 3: Contact / Socials -->
        <div class="p-6 md:p-12 flex flex-col justify-between">
          <div>
            <h2 class="uppercase tracking-widest text-xs mb-8 text-black/50">Contact</h2>
            <div class="space-y-4 font-serif text-xl sm:text-2xl text-black">
              <p>Email: <a href="mailto:faqihshiam23@gmail.com" class="hover:text-blue-600 transition-colors">faqihshiam23@gmail.com</a></p>
              <p>LinkedIn: <a href="https://www.linkedin.com/in/muhammadfaqihshiam23/" class="hover:text-blue-600 transition-colors" target="_blank" rel="noopener noreferrer">@muhammadfaqihshiam23</a></p>
              <p>Github: <a href="https://github.com/Dwdun" class="hover:text-blue-600 transition-colors" target="_blank" rel="noopener noreferrer">github.com/Dwdun</a></p>
            </div>
          </div>
          
          <div class="mt-16">
            <a href="/docs/CV.pdf" download="CV_Kreatif_Muhammad_Faqih_Shiam.pdf" class="inline-block font-sans text-sm tracking-wider text-black border-b border-black hover:opacity-50 transition-opacity">
              Download my CV →
            </a>
          </div>
        </div>

      </div>
    </section>

    <!-- Minimal Footer -->
    <footer class="border-t border-black/20 w-full py-6 px-6 md:px-12 mt-auto">
      <div class="flex flex-col sm:flex-row justify-between items-center text-sm font-sans text-black/60">
        <p>© 2026 {{ profile?.name }}. All rights reserved.</p>
        <div class="space-x-4 mt-4 sm:mt-0">
          <NuxtLink to="/profile" class="hover:text-black transition-colors">Profile</NuxtLink>
          <NuxtLink to="/contact" class="hover:text-black transition-colors">Contact</NuxtLink>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
const { profile, skills, achievements, projects } = useConfig()

const mouseX = ref(0)
const mouseY = ref(0)

const handle3DMove = (data: { x: number, y: number }) => {
  mouseX.value = data.x
  mouseY.value = data.y
}

// SEO
useHead({
  title: 'Home | Muhammad Faqih Shiam',
  meta: [{ name: 'description', content: 'Full-Stack Software Engineer portfolio' }]
})
</script>

<style scoped>
/* Animated Metallic Glass Gray Hover Effect */
.hover-metallic {
  display: inline-block;
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1), text-shadow 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  padding: 0 0.05em; /* prevents font clipping during transform */
}

.hover-metallic:hover {
  /* Darker gradient for "metallic glass gray" against a white background */
  background: linear-gradient(90deg, #4b5563 0%, #d1d5db 50%, #4b5563 100%);
  background-size: 200% auto;
  color: transparent !important;
  -webkit-background-clip: text;
  background-clip: text;
  animation: shine 2.5s linear infinite;
  transform: scale(1.05) translateY(-2px);
  text-shadow: 0 4px 15px rgba(0, 0, 0, 0.15);
}

/* Ensure any nested spans inherit the transparent mask on hover */
.hover-metallic:hover * {
  color: transparent !important;
  -webkit-text-fill-color: transparent !important;
}

@keyframes shine {
  to {
    background-position: 200% center;
  }
}

/* 3D Carousel Styles */
.scene, .a3d {
  display: grid;
}

.scene {
  overflow: hidden;
  perspective: 35em;
  mask: linear-gradient(90deg, transparent, red 20% 80%, transparent);
  -webkit-mask: linear-gradient(90deg, transparent, red 20% 80%, transparent);
}

.a3d {
  place-self: center;
  transform-style: preserve-3d;
  animation: ry 32s linear infinite;
}

@keyframes ry {
  to {
    transform: rotateY(1turn);
  }
}

.card-3d {
  --w: 12em; /* Smaller base sizing */
  --ba: 1turn/var(--n);
  grid-area: 1/1;
  width: var(--w);
  aspect-ratio: 7/9;
  object-fit: cover;
  border-radius: 0.5em; /* Sharper corners for brutalism */
  backface-visibility: hidden;
  transform: rotatey(calc(var(--i)*var(--ba))) translatez(calc(-1*(.5*var(--w) + .5em)/tan(.5*var(--ba))));
}

@media (min-width: 768px) {
  .card-3d {
    --w: 16em;
  }
}

@media (prefers-reduced-motion: reduce) {
  .a3d {
    animation-duration: 128s;
  }
}
</style>
