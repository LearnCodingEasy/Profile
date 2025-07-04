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
                    class="icons w-12 h-12 bg-white dark:bg-gray-700 rounded-full flex items-center justify-center hover:bg-blue-600 hover:text-white transform hover:scale-110 transition-all duration-300 shadow-lg"
                  >
                    <div v-html="getSocialIcon(social.name)" class="w-6 h-6 hover:text-white"></div>
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
  location: 'Cairo, Egypt,',
  quote: 'Code is poetry written in logic, and I love crafting digital experiences that inspire.',
  image: new URL('./assets/Hossam-Rashad.jpg', import.meta.url).href,
  
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
    email: 'learncodingeasy0100@gmail.com',
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
      // image: 'https://placehold.co/200x300?text=Placeholder',
      image: new URL('./assets/E-Commerce.png', import.meta.url).href,

      technologies: ['Vue.js', 'Node.js', 'MongoDB', 'Stripe API'],
      liveUrl: 'https://demo.example.com',
      githubUrl: 'https://github.com/example/ecommerce',
    },
    {
      id: 2,
      title: 'Task Management SaaS',
      description:
        'A collaborative project management tool with real-time updates, team collaboration features, and advanced analytics.',
      // image: 'https://placehold.co/200x300?text=Placeholder',
      image: new URL('./assets/Task _Management_SaaS.png', import.meta.url).href,

      technologies: ['React', 'TypeScript', 'Firebase', 'Material-UI'],
      liveUrl: 'https://demo.example.com',
      githubUrl: 'https://github.com/example/taskmanager',
    },
    {
      id: 3,
      title: 'AI-Powered Analytics',
      description:
        'A data visualization platform that uses machine learning to provide insights and predictive analytics for businesses.',
      // image: 'https://placehold.co/200x300?text=Placeholder',
      image: new URL('./assets/AI_Powered_Analytics.jpeg', import.meta.url).href,

      technologies: ['Python', 'Django', 'TensorFlow', 'D3.js'],
      liveUrl: 'https://demo.example.com',
      githubUrl: 'https://github.com/example/analytics',
    },
    {
      id: 4,
      title: 'Social Media Dashboard',
      description:
        'A comprehensive social media management tool with scheduling, analytics, and multi-platform integration.',
      // image: 'https://placehold.co/200x300?text=Placeholder',
      image: new URL('./assets/Social_Media_Dashboard.jpg', import.meta.url).href,

      technologies: ['Vue.js', 'Nuxt.js', 'PostgreSQL', 'Redis'],
      liveUrl: 'https://demo.example.com',
      githubUrl: 'https://github.com/example/socialdash',
    },
    {
      id: 5,
      title: 'Cryptocurrency Tracker',
      description:
        'A real-time cryptocurrency tracking application with portfolio management and price alerts.',
      // image: 'https://placehold.co/200x300?text=Placeholder',
      image: new URL('./assets/Cryptocurrency_Tracker.jpg', import.meta.url).href,

      technologies: ['React Native', 'Redux', 'CoinGecko API', 'Chart.js'],
      liveUrl: 'https://demo.example.com',
      githubUrl: 'https://github.com/example/cryptotracker',
    },
    {
      id: 6,
      title: 'Learning Management System',
      description:
        'An educational platform with course creation, student progress tracking, and interactive learning modules.',
      // image: 'https://placehold.co/200x300?text=Placeholder',
      image: new URL('./assets/Learning_Management_System.jpg', import.meta.url).href,
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
    github: `<svg viewBox="0 0 20 20" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" fill="#000000"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <title>github [#142]</title> <desc>Created with Sketch.</desc> <defs> </defs> <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd"> <g id="Dribbble-Light-Preview" transform="translate(-140.000000, -7559.000000)" fill="#000000"> <g id="icons" transform="translate(56.000000, 160.000000)"> <path d="M94,7399 C99.523,7399 104,7403.59 104,7409.253 C104,7413.782 101.138,7417.624 97.167,7418.981 C96.66,7419.082 96.48,7418.762 96.48,7418.489 C96.48,7418.151 96.492,7417.047 96.492,7415.675 C96.492,7414.719 96.172,7414.095 95.813,7413.777 C98.04,7413.523 100.38,7412.656 100.38,7408.718 C100.38,7407.598 99.992,7406.684 99.35,7405.966 C99.454,7405.707 99.797,7404.664 99.252,7403.252 C99.252,7403.252 98.414,7402.977 96.505,7404.303 C95.706,7404.076 94.85,7403.962 94,7403.958 C93.15,7403.962 92.295,7404.076 91.497,7404.303 C89.586,7402.977 88.746,7403.252 88.746,7403.252 C88.203,7404.664 88.546,7405.707 88.649,7405.966 C88.01,7406.684 87.619,7407.598 87.619,7408.718 C87.619,7412.646 89.954,7413.526 92.175,7413.785 C91.889,7414.041 91.63,7414.493 91.54,7415.156 C90.97,7415.418 89.522,7415.871 88.63,7414.304 C88.63,7414.304 88.101,7413.319 87.097,7413.247 C87.097,7413.247 86.122,7413.234 87.029,7413.87 C87.029,7413.87 87.684,7414.185 88.139,7415.37 C88.139,7415.37 88.726,7417.2 91.508,7416.58 C91.513,7417.437 91.522,7418.245 91.522,7418.489 C91.522,7418.76 91.338,7419.077 90.839,7418.982 C86.865,7417.627 84,7413.783 84,7409.253 C84,7403.59 88.478,7399 94,7399" id="github-[#142]"> </path> </g> </g> </g> </g></svg>`,
    linkedin: `<svg fill="#000000" version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="-143 145 512 512" xml:space="preserve"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <path d="M329,145h-432c-22.1,0-40,17.9-40,40v432c0,22.1,17.9,40,40,40h432c22.1,0,40-17.9,40-40V185C369,162.9,351.1,145,329,145z M41.4,508.1H-8.5V348.4h49.9V508.1z M15.1,328.4h-0.4c-18.1,0-29.8-12.2-29.8-27.7c0-15.8,12.1-27.7,30.5-27.7 c18.4,0,29.7,11.9,30.1,27.7C45.6,316.1,33.9,328.4,15.1,328.4z M241,508.1h-56.6v-82.6c0-21.6-8.8-36.4-28.3-36.4 c-14.9,0-23.2,10-27,19.6c-1.4,3.4-1.2,8.2-1.2,13.1v86.3H71.8c0,0,0.7-146.4,0-159.7h56.1v25.1c3.3-11,21.2-26.6,49.8-26.6 c35.5,0,63.3,23,63.3,72.4V508.1z"></path> </g></svg>`,
    twitter: `<svg fill="#000000" version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="-143 145 512 512" xml:space="preserve"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <path d="M329,145h-432c-22.1,0-40,17.9-40,40v432c0,22.1,17.9,40,40,40h432c22.1,0,40-17.9,40-40V185C369,162.9,351.1,145,329,145z M215.2,361.2c0.1,2.2,0.1,4.5,0.1,6.8c0,69.5-52.9,149.7-149.7,149.7c-29.7,0-57.4-8.7-80.6-23.6c4.1,0.5,8.3,0.7,12.6,0.7 c24.6,0,47.3-8.4,65.3-22.5c-23-0.4-42.5-15.6-49.1-36.5c3.2,0.6,6.5,0.9,9.9,0.9c4.8,0,9.5-0.6,13.9-1.9 C13.5,430-4.6,408.7-4.6,383.2v-0.6c7.1,3.9,15.2,6.3,23.8,6.6c-14.1-9.4-23.4-25.6-23.4-43.8c0-9.6,2.6-18.7,7.1-26.5 c26,31.9,64.7,52.8,108.4,55c-0.9-3.8-1.4-7.8-1.4-12c0-29,23.6-52.6,52.6-52.6c15.1,0,28.8,6.4,38.4,16.6 c12-2.4,23.2-6.7,33.4-12.8c-3.9,12.3-12.3,22.6-23.1,29.1c10.6-1.3,20.8-4.1,30.2-8.3C234.4,344.5,225.5,353.7,215.2,361.2z"></path> </g></svg>`,
    instagram: `<svg fill="#000000" version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="-143 145 512 512" xml:space="preserve"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <g> <path d="M113,446c24.8,0,45.1-20.2,45.1-45.1c0-9.8-3.2-18.9-8.5-26.3c-8.2-11.3-21.5-18.8-36.5-18.8s-28.3,7.4-36.5,18.8 c-5.3,7.4-8.5,16.5-8.5,26.3C68,425.8,88.2,446,113,446z"></path> <polygon points="211.4,345.9 211.4,308.1 211.4,302.5 205.8,302.5 168,302.6 168.2,346 "></polygon> <path d="M329,145h-432c-22.1,0-40,17.9-40,40v432c0,22.1,17.9,40,40,40h432c22.1,0,40-17.9,40-40V185C369,162.9,351.1,145,329,145z M241,374.7v104.8c0,27.3-22.2,49.5-49.5,49.5h-157C7.2,529-15,506.8-15,479.5V374.7v-52.3c0-27.3,22.2-49.5,49.5-49.5h157 c27.3,0,49.5,22.2,49.5,49.5V374.7z"></path> <path d="M183,401c0,38.6-31.4,70-70,70c-38.6,0-70-31.4-70-70c0-9.3,1.9-18.2,5.2-26.3H10v104.8C10,493,21,504,34.5,504h157 c13.5,0,24.5-11,24.5-24.5V374.7h-38.2C181.2,382.8,183,391.7,183,401z"></path> </g> </g></svg>`,
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
