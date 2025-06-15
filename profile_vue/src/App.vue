<template>
  <div :class="{ dark: isDarkMode }" class="min-h-screen transition-colors duration-300">
    <div class="bg-white dark:bg-gray-900 text-gray-900 dark:text-white min-h-screen">
      <!-- Sticky Header -->
      <header
        class="sticky top-0 z-50 bg-white/80 dark:bg-gray-900/80 backdrop-blur-md border-b border-gray-200 dark:border-gray-700"
      >
        <div class="container mx-auto px-4 py-4 flex justify-between items-center">
          <h1 class="text-xl font-bold">{{ profile.name }}</h1>
          <button
            @click="toggleDarkMode"
            class="p-2 rounded-lg bg-gray-100 dark:bg-gray-800 hover:bg-gray-200 dark:hover:bg-gray-700 transition-colors"
            aria-label="Toggle dark mode"
          >
            <svg v-if="isDarkMode" class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20">
              <path
                fill-rule="evenodd"
                d="M10 2a1 1 0 011 1v1a1 1 0 11-2 0V3a1 1 0 011-1zm4 8a4 4 0 11-8 0 4 4 0 018 0zm-.464 4.95l.707.707a1 1 0 001.414-1.414l-.707-.707a1 1 0 00-1.414 1.414zm2.12-10.607a1 1 0 010 1.414l-.706.707a1 1 0 11-1.414-1.414l.707-.707a1 1 0 011.414 0zM17 11a1 1 0 100-2h-1a1 1 0 100 2h1zm-7 4a1 1 0 011 1v1a1 1 0 11-2 0v-1a1 1 0 011-1zM5.05 6.464A1 1 0 106.465 5.05l-.708-.707a1 1 0 00-1.414 1.414l.707.707zm1.414 8.486l-.707.707a1 1 0 01-1.414-1.414l.707-.707a1 1 0 011.414 1.414zM4 11a1 1 0 100-2H3a1 1 0 000 2h1z"
                clip-rule="evenodd"
              ></path>
            </svg>
            <svg v-else class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20">
              <path d="M17.293 13.293A8 8 0 016.707 2.707a8.001 8.001 0 1010.586 10.586z"></path>
            </svg>
          </button>
        </div>
      </header>

      <!-- Hero/Profile Section -->
      <section
        class="py-20 bg-gradient-to-br from-blue-50 to-indigo-100 dark:from-gray-800 dark:to-gray-900"
      >
        <div class="container mx-auto px-4 text-center">
          <div class="max-w-4xl mx-auto">
            <!-- Profile Image -->
            <div class="relative inline-block mb-8">
              <img
                :src="profile.image"
                :alt="profile.name"
                class="w-32 h-32 md:w-40 md:h-40 rounded-full border-4 border-white dark:border-gray-700 shadow-xl object-cover mx-auto animate-pulse-slow"
              />
              <div
                class="absolute bottom-2 right-2 w-6 h-6 bg-green-400 rounded-full border-2 border-white dark:border-gray-700 animate-pulse"
              ></div>
            </div>

            <!-- Profile Info -->
            <h1
              class="text-4xl md:text-6xl font-bold mb-4 bg-gradient-to-r from-blue-600 to-purple-600 bg-clip-text text-transparent"
            >
              {{ profile.name }}
            </h1>
            <h2 class="text-xl md:text-2xl text-gray-600 dark:text-gray-300 mb-2">
              {{ profile.title }}
            </h2>
            <p class="text-gray-500 dark:text-gray-400 mb-4 flex items-center justify-center gap-2">
              <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 20 20">
                <path
                  fill-rule="evenodd"
                  d="M5.05 4.05a7 7 0 119.9 9.9L10 18.9l-4.95-4.95a7 7 0 010-9.9zM10 11a2 2 0 100-4 2 2 0 000 4z"
                  clip-rule="evenodd"
                ></path>
              </svg>
              {{ profile.location }}
            </p>
            <blockquote
              class="text-lg md:text-xl italic text-gray-700 dark:text-gray-300 mb-8 max-w-2xl mx-auto"
            >
              "{{ profile.quote }}"
            </blockquote>

            <!-- CTA Button -->
            <button
              @click="scrollToContact"
              class="bg-gradient-to-r from-blue-600 to-purple-600 text-white px-8 py-4 rounded-full font-semibold text-lg hover:from-blue-700 hover:to-purple-700 transform hover:scale-105 transition-all duration-300 shadow-lg hover:shadow-xl"
            >
              Hire Me
            </button>
          </div>
        </div>
      </section>

      <!-- About Me Section -->
      <section class="py-20 bg-white dark:bg-gray-900">
        <div class="container mx-auto px-4">
          <div class="max-w-4xl mx-auto">
            <h2 class="text-3xl md:text-4xl font-bold text-center mb-12">About Me</h2>
            <div class="grid md:grid-cols-2 gap-12 items-center">
              <div>
                <p class="text-lg text-gray-600 dark:text-gray-300 leading-relaxed mb-6">
                  {{ profile.about.description }}
                </p>
                <p class="text-lg text-gray-600 dark:text-gray-300 leading-relaxed">
                  {{ profile.about.background }}
                </p>
              </div>
              <div>
                <h3 class="text-xl font-semibold mb-6">Interests & Passions</h3>
                <div class="grid grid-cols-2 gap-4">
                  <div
                    v-for="interest in profile.interests"
                    :key="interest.name"
                    class="flex items-center gap-3 p-3 bg-gray-50 dark:bg-gray-800 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-700 transition-colors"
                  >
                    <span class="text-2xl">{{ interest.icon }}</span>
                    <span class="font-medium">{{ interest.name }}</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- Contact Information -->
      <section id="contact" class="py-20 bg-gray-50 dark:bg-gray-800">
        <div class="container mx-auto px-4">
          <div class="max-w-4xl mx-auto text-center">
            <h2 class="text-3xl md:text-4xl font-bold mb-12">Get In Touch</h2>
            <div class="grid md:grid-cols-2 gap-8 mb-12">
              <!-- Contact Info -->
              <div class="space-y-6">
                <div class="flex items-center justify-center md:justify-start gap-4">
                  <svg class="w-6 h-6 text-blue-600" fill="currentColor" viewBox="0 0 20 20">
                    <path
                      d="M2.003 5.884L10 9.882l7.997-3.998A2 2 0 0016 4H4a2 2 0 00-1.997 1.884z"
                    ></path>
                    <path d="M18 8.118l-8 4-8-4V14a2 2 0 002 2h12a2 2 0 002-2V8.118z"></path>
                  </svg>
                  <a
                    :href="`mailto:${profile.contact.email}`"
                    class="text-lg hover:text-blue-600 transition-colors"
                  >
                    {{ profile.contact.email }}
                  </a>
                </div>
                <div class="flex items-center justify-center md:justify-start gap-4">
                  <svg class="w-6 h-6 text-blue-600" fill="currentColor" viewBox="0 0 20 20">
                    <path
                      d="M2 3a1 1 0 011-1h2.153a1 1 0 01.986.836l.74 4.435a1 1 0 01-.54 1.06l-1.548.773a11.037 11.037 0 006.105 6.105l.774-1.548a1 1 0 011.059-.54l4.435.74a1 1 0 01.836.986V17a1 1 0 01-1 1h-2C7.82 18 2 12.18 2 5V3z"
                    ></path>
                  </svg>
                  <a
                    :href="`tel:${profile.contact.phone}`"
                    class="text-lg hover:text-blue-600 transition-colors"
                  >
                    {{ profile.contact.phone }}
                  </a>
                </div>
              </div>

              <!-- Social Media -->
              <div>
                <h3 class="text-xl font-semibold mb-6">Follow Me</h3>
                <div class="flex justify-center md:justify-start gap-4">
                  <a
                    v-for="social in profile.social"
                    :key="social.name"
                    :href="social.url"
                    target="_blank"
                    class="w-12 h-12 bg-white dark:bg-gray-700 rounded-full flex items-center justify-center hover:bg-blue-600 hover:text-white transform hover:scale-110 transition-all duration-300 shadow-lg"
                  >
                    <component :is="getSocialIcon(social.name)" class="w-6 h-6" />
                  </a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- Skills Section -->
      <section class="py-20 bg-white dark:bg-gray-900">
        <div class="container mx-auto px-4">
          <div class="max-w-6xl mx-auto">
            <h2 class="text-3xl md:text-4xl font-bold text-center mb-12">Skills & Expertise</h2>

            <!-- Technical Skills -->
            <div class="mb-16">
              <h3 class="text-2xl font-semibold mb-8 text-center">Technical Skills</h3>
              <div class="grid md:grid-cols-2 gap-8">
                <div v-for="skill in profile.skills.technical" :key="skill.name" class="space-y-2">
                  <div class="flex justify-between">
                    <span class="font-medium">{{ skill.name }}</span>
                    <span class="text-gray-500">{{ skill.level }}%</span>
                  </div>
                  <div class="w-full bg-gray-200 dark:bg-gray-700 rounded-full h-3">
                    <div
                      class="bg-gradient-to-r from-blue-500 to-purple-500 h-3 rounded-full transition-all duration-1000 ease-out"
                      :style="{ width: `${skill.level}%` }"
                    ></div>
                  </div>
                </div>
              </div>
            </div>

            <!-- Soft Skills -->
            <div>
              <h3 class="text-2xl font-semibold mb-8 text-center">Soft Skills</h3>
              <div class="flex flex-wrap justify-center gap-4">
                <span
                  v-for="skill in profile.skills.soft"
                  :key="skill"
                  class="px-6 py-3 bg-gradient-to-r from-blue-100 to-purple-100 dark:from-blue-900 dark:to-purple-900 text-blue-800 dark:text-blue-200 rounded-full font-medium hover:from-blue-200 hover:to-purple-200 dark:hover:from-blue-800 dark:hover:to-purple-800 transition-all duration-300"
                >
                  {{ skill }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- Portfolio Section -->
      <section class="py-20 bg-gray-50 dark:bg-gray-800">
        <div class="container mx-auto px-4">
          <div class="max-w-6xl mx-auto">
            <h2 class="text-3xl md:text-4xl font-bold text-center mb-12">Featured Projects</h2>
            <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
              <div
                v-for="project in profile.portfolio"
                :key="project.id"
                class="bg-white dark:bg-gray-900 rounded-xl shadow-lg hover:shadow-2xl transform hover:-translate-y-2 transition-all duration-300 overflow-hidden group"
              >
                <div class="relative overflow-hidden">
                  <img
                    :src="project.image"
                    :alt="project.title"
                    class="w-full h-48 object-cover group-hover:scale-110 transition-transform duration-300"
                  />
                  <div
                    class="absolute inset-0 bg-gradient-to-t from-black/50 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"
                  ></div>
                </div>
                <div class="p-6">
                  <h3 class="text-xl font-bold mb-3">{{ project.title }}</h3>
                  <p class="text-gray-600 dark:text-gray-300 mb-4 line-clamp-3">
                    {{ project.description }}
                  </p>
                  <div class="flex flex-wrap gap-2 mb-4">
                    <span
                      v-for="tech in project.technologies"
                      :key="tech"
                      class="px-3 py-1 bg-blue-100 dark:bg-blue-900 text-blue-800 dark:text-blue-200 text-sm rounded-full"
                    >
                      {{ tech }}
                    </span>
                  </div>
                  <div class="flex gap-4">
                    <a
                      :href="project.liveUrl"
                      target="_blank"
                      class="flex-1 bg-blue-600 text-white text-center py-2 rounded-lg hover:bg-blue-700 transition-colors font-medium"
                    >
                      Live Demo
                    </a>
                    <a
                      :href="project.githubUrl"
                      target="_blank"
                      class="flex-1 border border-gray-300 dark:border-gray-600 text-center py-2 rounded-lg hover:bg-gray-50 dark:hover:bg-gray-700 transition-colors font-medium"
                    >
                      GitHub
                    </a>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- Footer -->
      <footer class="py-12 bg-gray-900 text-white">
        <div class="container mx-auto px-4 text-center">
          <p class="mb-4">&copy; {{ currentYear }} {{ profile.name }}. All rights reserved.</p>
          <button
            @click="scrollToTop"
            class="inline-flex items-center gap-2 bg-blue-600 hover:bg-blue-700 px-4 py-2 rounded-lg transition-colors"
          >
            <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 20 20">
              <path
                fill-rule="evenodd"
                d="M3.293 9.707a1 1 0 010-1.414l6-6a1 1 0 011.414 0l6 6a1 1 0 01-1.414 1.414L11 5.414V17a1 1 0 11-2 0V5.414L4.707 9.707a1 1 0 01-1.414 0z"
                clip-rule="evenodd"
              ></path>
            </svg>
            Back to Top
          </button>
        </div>
      </footer>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

// Dark mode state
const isDarkMode = ref(false)

// Profile data
const profile = ref({
  name: 'Hossam Rashad',
  title: 'Full-Stack Developer',
  location: 'San Francisco, CA',
  quote: 'Code is poetry written in logic, and I love crafting digital experiences that inspire.',
  image: './../../assets/Images/My.jpg',
  about: {
    description:
      "I'm a passionate full-stack developer with 6+ years of experience building scalable web applications. I specialize in modern JavaScript frameworks and love turning complex problems into simple, beautiful solutions.",
    background:
      "When I'm not coding, you'll find me exploring new technologies, contributing to open-source projects, or sharing knowledge through technical writing and mentoring junior developers.",
  },
  interests: [
    { name: 'Web Development', icon: '💻' },
    { name: 'Open Source', icon: '🚀' },
    { name: 'Photography', icon: '📸' },
    { name: 'Travel', icon: '✈️' },
    { name: 'Music', icon: '🎵' },
    { name: 'Gaming', icon: '🎮' },
  ],
  contact: {
    email: 'alex.rodriguez@email.com',
    phone: '+02 01091642528',
  },
  social: [
    { name: 'github', url: 'https://github.com/LearnCodingEasy' },
    { name: 'linkedin', url: 'https://linkedin.com/in/alexrodriguez' },
    { name: 'twitter', url: 'https://twitter.com/alexrodriguez' },
    { name: 'instagram', url: 'https://instagram.com/alexrodriguez' },
  ],
  skills: {
    technical: [
      { name: 'Vue.js', level: 95 },
      { name: 'React', level: 90 },
      { name: 'TypeScript', level: 88 },
      { name: 'Node.js', level: 85 },
      { name: 'Python', level: 82 },
      { name: 'Tailwind CSS', level: 92 },
      { name: 'GraphQL', level: 78 },
      { name: 'MongoDB', level: 80 },
    ],
    soft: [
      'Problem Solving',
      'Team Leadership',
      'Communication',
      'Project Management',
      'Mentoring',
      'Creative Thinking',
    ],
  },
  portfolio: [
    {
      id: 1,
      title: 'E-Commerce Platform',
      description:
        'A full-featured e-commerce platform with real-time inventory management, payment processing, and admin dashboard.',
      image: '/placeholder.svg?height=200&width=300',
      technologies: ['Vue.js', 'Node.js', 'MongoDB', 'Stripe API'],
      liveUrl: 'https://demo.example.com',
      githubUrl: 'https://github.com/example/ecommerce',
    },
    {
      id: 2,
      title: 'Task Management SaaS',
      description:
        'A collaborative project management tool with real-time updates, team collaboration features, and advanced analytics.',
      image: '/placeholder.svg?height=200&width=300',
      technologies: ['React', 'TypeScript', 'Firebase', 'Material-UI'],
      liveUrl: 'https://demo.example.com',
      githubUrl: 'https://github.com/example/taskmanager',
    },
    {
      id: 3,
      title: 'AI-Powered Analytics',
      description:
        'A data visualization platform that uses machine learning to provide insights and predictive analytics for businesses.',
      image: '/placeholder.svg?height=200&width=300',
      technologies: ['Python', 'Django', 'TensorFlow', 'D3.js'],
      liveUrl: 'https://demo.example.com',
      githubUrl: 'https://github.com/example/analytics',
    },
    {
      id: 4,
      title: 'Social Media Dashboard',
      description:
        'A comprehensive social media management tool with scheduling, analytics, and multi-platform integration.',
      image: '/placeholder.svg?height=200&width=300',
      technologies: ['Vue.js', 'Nuxt.js', 'PostgreSQL', 'Redis'],
      liveUrl: 'https://demo.example.com',
      githubUrl: 'https://github.com/example/socialdash',
    },
    {
      id: 5,
      title: 'Cryptocurrency Tracker',
      description:
        'A real-time cryptocurrency tracking application with portfolio management and price alerts.',
      image: '/placeholder.svg?height=200&width=300',
      technologies: ['React Native', 'Redux', 'CoinGecko API', 'Chart.js'],
      liveUrl: 'https://demo.example.com',
      githubUrl: 'https://github.com/example/cryptotracker',
    },
    {
      id: 6,
      title: 'Learning Management System',
      description:
        'An educational platform with course creation, student progress tracking, and interactive learning modules.',
      image: '/placeholder.svg?height=200&width=300',
      technologies: ['Vue.js', 'Laravel', 'MySQL', 'WebRTC'],
      liveUrl: 'https://demo.example.com',
      githubUrl: 'https://github.com/example/lms',
    },
  ],
})

// Computed properties
const currentYear = computed(() => new Date().getFullYear())

// Methods
const toggleDarkMode = () => {
  isDarkMode.value = !isDarkMode.value
  localStorage.setItem('darkMode', isDarkMode.value.toString())
}

const scrollToContact = () => {
  document.getElementById('contact')?.scrollIntoView({ behavior: 'smooth' })
}

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

// Social icon components
const getSocialIcon = (name) => {
  const icons = {
    github: () => ({
      template: `<svg fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 0C4.477 0 0 4.484 0 10.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0110 4.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.203 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.942.359.31.678.921.678 1.856 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0020 10.017C20 4.484 15.522 0 10 0z" clip-rule="evenodd"></path></svg>`,
    }),
    linkedin: () => ({
      template: `<svg fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M16.338 16.338H13.67V12.16c0-.995-.017-2.277-1.387-2.277-1.39 0-1.601 1.086-1.601 2.207v4.248H8.014v-8.59h2.559v1.174h.037c.356-.675 1.227-1.387 2.526-1.387 2.703 0 3.203 1.778 3.203 4.092v4.711zM5.005 6.575a1.548 1.548 0 11-.003-3.096 1.548 1.548 0 01.003 3.096zm-1.337 9.763H6.34v-8.59H3.667v8.59zM17.668 1H2.328C1.595 1 1 1.581 1 2.298v15.403C1 18.418 1.595 19 2.328 19h15.34c.734 0 1.332-.582 1.332-1.299V2.298C19 1.581 18.402 1 17.668 1z" clip-rule="evenodd"></path></svg>`,
    }),
    twitter: () => ({
      template: `<svg fill="currentColor" viewBox="0 0 20 20"><path d="M6.29 18.251c7.547 0 11.675-6.253 11.675-11.675 0-.178 0-.355-.012-.53A8.348 8.348 0 0020 3.92a8.19 8.19 0 01-2.357.646 4.118 4.118 0 001.804-2.27 8.224 8.224 0 01-2.605.996 4.107 4.107 0 00-6.993 3.743 11.65 11.65 0 01-8.457-4.287 4.106 4.106 0 001.27 5.477A4.073 4.073 0 01.8 7.713v.052a4.105 4.105 0 003.292 4.022 4.095 4.095 0 01-1.853.07 4.108 4.108 0 003.834 2.85A8.233 8.233 0 010 16.407a11.616 11.616 0 006.29 1.84"></path></svg>`,
    }),
    instagram: () => ({
      template: `<svg fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 0C7.284 0 6.944.012 5.877.06 2.246.227.227 2.242.06 5.877.012 6.944 0 7.284 0 10s.012 3.056.06 4.123c.167 3.632 2.182 5.65 5.817 5.817C6.944 19.988 7.284 20 10 20s3.056-.012 4.123-.06c3.629-.167 5.652-2.182 5.817-5.817C19.988 13.056 20 12.716 20 10s-.012-3.056-.06-4.123C19.833 2.245 17.815.227 14.183.06 13.056.012 12.716 0 10 0zm0 1.802c2.67 0 2.987.01 4.042.059 2.71.123 3.975 1.409 4.099 4.099.048 1.054.057 1.37.057 4.04 0 2.672-.01 2.988-.057 4.042-.124 2.687-1.387 3.975-4.1 4.099-1.054.048-1.37.058-4.041.058-2.67 0-2.987-.01-4.04-.058-2.717-.124-3.977-1.416-4.1-4.1-.048-1.054-.058-1.37-.058-4.041 0-2.67.01-2.986.058-4.04.124-2.69 1.387-3.977 4.1-4.1 1.054-.048 1.37-.058 4.04-.058zM10 4.865a5.135 5.135 0 100 10.27 5.135 5.135 0 000-10.27zm0 8.468a3.333 3.333 0 110-6.666 3.333 3.333 0 010 6.666zm5.338-9.87a1.2 1.2 0 100 2.4 1.2 1.2 0 000-2.4z" clip-rule="evenodd"></path></svg>`,
    }),
  }
  return icons[name] || icons.github
}

// Initialize dark mode from localStorage
onMounted(() => {
  const savedDarkMode = localStorage.getItem('darkMode')
  if (savedDarkMode !== null) {
    isDarkMode.value = savedDarkMode === 'true'
  } else {
    // Check system preference
    isDarkMode.value = window.matchMedia('(prefers-color-scheme: dark)').matches
  }
})
</script>

<style scoped></style>
