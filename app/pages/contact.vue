<template>
  <div class="min-h-screen bg-transparent pt-32 pb-24 px-6 md:px-12 max-w-[1400px] mx-auto">
    <div v-if="profile" class="grid grid-cols-1 lg:grid-cols-12 gap-16 lg:gap-8">
      
      <!-- Left Column: Typography & Info -->
      <div class="lg:col-span-5 lg:pr-12">
        <h1 class="font-serif text-[4rem] md:text-[6rem] leading-none text-black mb-12">
          Get<br>In Touch
        </h1>

        <div class="space-y-12">
          <!-- Availability Tag -->
          <div class="flex items-center space-x-3">
            <span class="relative flex h-3 w-3">
              <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-blue-400 opacity-75"></span>
              <span class="relative inline-flex rounded-full h-3 w-3 bg-blue-600"></span>
            </span>
            <p class="font-sans text-sm uppercase tracking-widest text-black/60">Available for Opportunities</p>
          </div>

          <!-- Contact Details (Text-based Brutalism) -->
          <div class="font-serif text-2xl md:text-3xl text-black space-y-4">
            <div class="group flex items-center justify-between border-b border-black/10 pb-4">
              <span class="text-black/50 font-sans text-sm tracking-widest uppercase">Email</span>
              <a :href="`mailto:${profile.contact.email}`" class="hover:text-blue-600 transition-colors">{{ profile.contact.email }}</a>
            </div>
            
            <div class="group flex items-center justify-between border-b border-black/10 pb-4">
              <span class="text-black/50 font-sans text-sm tracking-widest uppercase">Phone</span>
              <a :href="`tel:${profile.contact.phone}`" class="hover:text-blue-600 transition-colors">{{ profile.contact.phone }}</a>
            </div>

            <div class="group flex items-center justify-between border-b border-black/10 pb-4">
              <span class="text-black/50 font-sans text-sm tracking-widest uppercase">Location</span>
              <span class="text-right">{{ profile.contact.location }}</span>
            </div>
          </div>

          <!-- Socials Grid -->
          <div class="pt-8">
            <p class="font-sans text-sm uppercase tracking-widest text-black/50 mb-6">Socials</p>
            <div class="grid grid-cols-2 gap-4">
              <a 
                v-for="social in profile.socialLinks" 
                :key="social.platform"
                :href="social.url"
                target="_blank"
                class="font-sans text-lg text-black hover:text-blue-600 border border-black/20 p-4 text-center hover:bg-black/[0.02] transition-colors"
                >
                {{ social.platform }} ↗
              </a>
              <a href="https://github.com/Dwdun" target="_blank" class="font-sans text-lg text-black hover:text-blue-600 border border-black/20 p-4 text-center hover:bg-black/[0.02] transition-colors">
                GitHub ↗
              </a>
            </div>
          </div>

        </div>
      </div>

      <!-- Right Column: Minimal Form -->
      <div class="lg:col-span-7 bg-white p-8 md:p-16 border border-black/10 shadow-2xl relative">
        <h2 class="font-serif text-3xl mb-8 text-black">Send a message</h2>
        
        <form @submit.prevent="handleSubmit" class="space-y-8 font-sans">
          <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
            <div class="space-y-2">
              <label for="name" class="text-xs uppercase tracking-widest text-black/50">Name</label>
              <input
                id="name"
                v-model="form.name"
                type="text"
                required
                class="w-full bg-transparent border-b border-black/20 pb-2 text-black focus:outline-none focus:border-blue-600 transition-colors placeholder-black/20"
                placeholder="John Doe"
              />
            </div>

            <div class="space-y-2">
              <label for="email" class="text-xs uppercase tracking-widest text-black/50">Email</label>
              <input
                id="email"
                v-model="form.email"
                type="email"
                required
                class="w-full bg-transparent border-b border-black/20 pb-2 text-black focus:outline-none focus:border-blue-600 transition-colors placeholder-black/20"
                placeholder="hello@example.com"
              />
            </div>
          </div>

          <div class="space-y-2">
            <label for="subject" class="text-xs uppercase tracking-widest text-black/50">Subject</label>
            <input
              id="subject"
              v-model="form.subject"
              type="text"
              required
              class="w-full bg-transparent border-b border-black/20 pb-2 text-black focus:outline-none focus:border-blue-600 transition-colors placeholder-black/20"
              placeholder="What's this about?"
            />
          </div>

          <div class="space-y-2">
            <label for="message" class="text-xs uppercase tracking-widest text-black/50">Message</label>
            <textarea
              id="message"
              v-model="form.message"
              required
              rows="4"
              class="w-full bg-transparent border-b border-black/20 pb-2 text-black focus:outline-none focus:border-blue-600 transition-colors resize-none placeholder-black/20"
              placeholder="Hello Muhammad, I have a project..."
            />
          </div>

          <button 
            type="submit" 
            :disabled="isSubmitting"
            class="w-full bg-black text-white font-sans uppercase tracking-widest text-sm py-4 hover:bg-blue-600 transition-colors disabled:opacity-50"
          >
            {{ isSubmitting ? 'Sending...' : 'Send Message →' }}
          </button>

          <div v-if="submitted" class="text-center font-serif text-blue-600 italic">
            Message sent! I'll get back to you soon.
          </div>
        </form>
      </div>

    </div>
  </div>
</template>

<script setup lang="ts">
const { profile } = useConfig()

const form = ref({
  name: '',
  email: '',
  subject: '',
  message: ''
})

const isSubmitting = ref(false)
const submitted = ref(false)

const handleSubmit = async () => {
  isSubmitting.value = true
  
  // Simulate form submission (in real app, send to backend/email service)
  await new Promise(resolve => setTimeout(resolve, 1500))
  
  // For demo purposes, just show success message
  // In production, integrate with email service or backend API
  console.log('Form submitted:', form.value)
  
  submitted.value = true
  isSubmitting.value = false
  
  // Reset form
  setTimeout(() => {
    form.value = { name: '', email: '', subject: '', message: '' }
    submitted.value = false
  }, 3000)
}

useHead({
  title: 'Contact | Muhammad Faqih Shiam',
  meta: [{ name: 'description', content: 'Get in touch for opportunities and collaborations' }]
})
</script>
