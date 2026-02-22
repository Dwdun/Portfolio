<template>
  <div class="min-h-screen bg-transparent overflow-x-hidden pt-12 md:pt-24">
    <!-- Hero Editorial Section -->
    <section class="max-w-[1400px] mx-auto px-6 sm:px-12 pb-16 md:pb-24 flex flex-col items-center justify-center text-center">
      
      <div v-if="profile" class="w-full relative z-10 flex flex-col items-center">
        <!-- Main Typographic Intro -->
        <h1 class="font-serif text-[2.5rem] sm:text-[4rem] md:text-[5rem] lg:text-[6rem] leading-[1.1] tracking-tight text-black max-w-5xl mx-auto mb-16">
          Hi there, I'm <span class="italic font-medium text-blue-600">{{ profile.name }}</span>. I'm a student based in Bandung who loves bringing ideas to life through <span class="italic">digital art</span>, <span class="text-blue-600">character illustrations</span>, and <span class="italic">game assets</span>. Welcome to my creative website.
        </h1>

        <!-- 3D Carousel Scene (Central Visual) -->
        <div class="scene w-full h-[300px] md:h-[500px] flex justify-center items-center mb-16 md:mb-32 perspective-[1000px]">
          <div class="a3d hover:scale-105 transition-transform duration-700" style="--n: 6">
            <img class="card-3d shadow-2xl border border-black/10" src="/assets/gambar/Cyrene.jpg" style="--i: 0" alt="Cyrene illustration"/>
            <img class="card-3d shadow-2xl border border-black/10" src="/assets/gambar/HCW_Poster.png" style="--i: 1" alt="HCW Poster"/>
            <img class="card-3d shadow-2xl border border-black/10" src="/assets/gambar/jacq update 2.png" style="--i: 2" alt="Jacq character artwork"/>
            <img class="card-3d shadow-2xl border border-black/10" src="/assets/gambar/kakavasha final.png" style="--i: 3" alt="Kakavasha character art"/>
            <img class="card-3d shadow-2xl border border-black/10" src="/assets/gambar/phainon final.png" style="--i: 4" alt="Phainon character art"/>
            <img class="card-3d shadow-2xl border border-black/10" src="/assets/gambar/sparxie final.png" style="--i: 5" alt="Sparxie character art"/>
          </div>
        </div>

        <!-- Read More Button -->
        <NuxtLink to="/portfolio" class="font-sans text-sm uppercase tracking-widest text-black hover:opacity-50 transition-opacity border-b border-black pb-1 mb-24">
          Read more →
        </NuxtLink>
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
              <p>Email: <a href="mailto:hello@example.com" class="hover:text-blue-600 transition-colors">hello@yourdomain.com</a></p>
              <p>LinkedIn: <a href="#" class="hover:text-blue-600 transition-colors">@yourname</a></p>
              <p>Github: <a href="#" class="hover:text-blue-600 transition-colors">yourgithub</a></p>
            </div>
          </div>
          
          <div class="mt-16">
            <NuxtLink to="/contact" class="inline-block font-sans text-sm tracking-wider text-black border-b border-black hover:opacity-50 transition-opacity">
              Download my CV →
            </NuxtLink>
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
const { profile, skills, achievements, projects } = useConfig()

// SEO
useHead({
  title: 'Home | Muhammad Faqih Shiam',
  meta: [{ name: 'description', content: 'Full-Stack Software Engineer portfolio' }]
})
</script>

<style scoped>
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
