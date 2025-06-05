<template>
  <section class="presentation-section" ref="sectionRef">
    <!-- Background Effects -->
    <div class="bg-effects">
      <div class="floating-orbs">
        <div v-for="n in 12" :key="n" class="orb" :style="getOrbStyle(n)"></div>
      </div>
      <div class="grid-overlay"></div>
      <div class="gradient-waves"></div>
    </div>

    <!-- Main Container -->
    <div class="presentation-container" :class="{ 'visible': isVisible }">
      <!-- Animated Border Container -->
      <div class="border-container">
        <svg class="border-svg" viewBox="0 0 100 100" preserveAspectRatio="none">
          <defs>
            <linearGradient id="borderGradient" x1="0%" y1="0%" x2="100%" y2="100%">
              <stop offset="0%" :style="`stop-color:${currentColors[0]};stop-opacity:1`" />
              <stop offset="25%" :style="`stop-color:${currentColors[1]};stop-opacity:1`" />
              <stop offset="50%" :style="`stop-color:${currentColors[2]};stop-opacity:1`" />
              <stop offset="75%" :style="`stop-color:${currentColors[3]};stop-opacity:1`" />
              <stop offset="100%" :style="`stop-color:${currentColors[0]};stop-opacity:1`" />
            </linearGradient>
          </defs>
          <rect x="1" y="1" width="98" height="98" 
                fill="none" 
                stroke="url(#borderGradient)" 
                stroke-width="0.5"
                class="animated-border-path" />
        </svg>
        
        <!-- Glass Container -->
        <div class="glass-container">
          <!-- Content Grid -->
          <div class="content-grid">
            <!-- Description Section -->
            <div class="desc-section" :class="{ 'animate-in': showDesc }">
              <DescComp />
            </div>
            
            <!-- Accounts Section -->
            <div class="accounts-section" :class="{ 'animate-in': showAccounts }">
              <AccountsComp />
            </div>
          </div>
          
    
        </div>
      </div>
    </div>

    <!-- Particle System -->
    <div class="particles-container">
      <div 
        v-for="particle in particles" 
        :key="particle.id"
        class="particle"
        :style="particle.style"
      ></div>
    </div>
  </section>
</template>

<script setup>
import { ref, reactive, onMounted, onUnmounted, watch } from 'vue'
import DescComp from './DescComp.vue'
import AccountsComp from './AccountsComp.vue'

// Reactive state
const sectionRef = ref(null)
const isVisible = ref(false)
const showDesc = ref(false)
const showAccounts = ref(false)
const isDarkTheme = ref(true)

// Color themes
const colorThemes = {
  dark: ['#d40c0c', '#8b0000', '#2e2e2e', '#1c1c1c'],
}

const currentColors = ref(colorThemes.dark)
// Particle system
const particles = reactive([])

// Methods
const getOrbStyle = (index) => {
  const delay = index * 0.5
  const duration = 8 + Math.random() * 4
  const size = 20 + Math.random() * 40
  const x = Math.random() * 100
  const y = Math.random() * 100
  
  return {
    '--delay': `${delay}s`,
    '--duration': `${duration}s`,
    '--size': `${size}px`,
    left: `${x}%`,
    top: `${y}%`,
    animationDelay: `${delay}s`,
    animationDuration: `${duration}s`
  }
}

const createParticle = () => {
  const id = Date.now() + Math.random()
  const particle = {
    id,
    style: {
      left: Math.random() * 100 + '%',
      animationDuration: (2 + Math.random() * 3) + 's',
      animationDelay: Math.random() * 2 + 's',
      opacity: 0.1 + Math.random() * 0.3
    }
  }
  
  particles.push(particle)
  
  setTimeout(() => {
    const index = particles.findIndex(p => p.id === id)
    if (index > -1) particles.splice(index, 1)
  }, 5000)
}
// Intersection Observer for animations
let observer = null

onMounted(() => {
  // Setup intersection observer
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          isVisible.value = true
          setTimeout(() => showDesc.value = true, 300)
          setTimeout(() => showAccounts.value = true, 600)
        }
      })
    },
    { threshold: 0.2 }
  )
  
  if (sectionRef.value) {
    observer.observe(sectionRef.value)
  }
  
  // Start particle system
  const particleInterval = setInterval(createParticle, 800)
  
  onUnmounted(() => {
    clearInterval(particleInterval)
    if (observer) observer.disconnect()
  })
})

// Watch theme changes
watch(isDarkTheme, (newTheme) => {
  document.documentElement.style.setProperty(
    '--theme-filter', 
    newTheme ? 'brightness(1)' : 'brightness(1.2) contrast(1.1)'
  )
})
</script>

<style scoped>
.presentation-section {
  position: relative;
  width: 100%;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  overflow: hidden;
  background: radial-gradient(ellipse at center, 
    rgba(15, 15, 35, 0.9) 0%, 
    rgba(5, 5, 15, 0.95) 70%, 
    rgba(0, 0, 0, 1) 100%);
}

/* Background Effects */
.bg-effects {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 1;
}

.floating-orbs {
  position: absolute;
  width: 100%;
  height: 100%;
}

.orb {
  position: absolute;
  width: var(--size);
  height: var(--size);
  border-radius: 50%;
  background: radial-gradient(circle at 30% 30%, 
    rgba(255, 255, 255, 0.2), 
    rgba(139, 0, 255, 0.1), 
    transparent);
  filter: blur(1px);
  animation: float var(--duration) ease-in-out infinite;
  animation-delay: var(--delay);
}

@keyframes float {
  0%, 100% { 
    transform: translateY(0px) rotate(0deg); 
    opacity: 0.3;
  }
  50% { 
    transform: translateY(-30px) rotate(180deg); 
    opacity: 0.8;
  }
}

.grid-overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-image: 
    linear-gradient(rgba(255, 255, 255, 0.02) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255, 255, 255, 0.02) 1px, transparent 1px);
  background-size: 50px 50px;
  animation: gridMove 20s linear infinite;
}

@keyframes gridMove {
  0% { transform: translate(0, 0); }
  100% { transform: translate(50px, 50px); }
}

.gradient-waves {
  position: absolute;
  width: 200%;
  height: 200%;
  background: conic-gradient(from 0deg, 
    transparent, 
    rgba(255, 0, 110, 0.03), 
    transparent, 
    rgba(131, 56, 236, 0.03), 
    transparent);
  animation: rotate 30s linear infinite;
  top: -50%;
  left: -50%;
}

@keyframes rotate {
  100% { transform: rotate(360deg); }
}

/* Main Container */
.presentation-container {
  position: relative;
  z-index: 10;
  max-width: 1400px;
  width: 100%;
  opacity: 0;
  transform: translateY(50px) scale(0.95);
  transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.presentation-container.visible {
  opacity: 1;
  transform: translateY(0) scale(1);
}

/* Border Container */
.border-container {
  position: relative;
  border-radius: 24px;
  padding: 3px;
  background: transparent;
  background-size: 400% 400%;
  animation: gradientShift 8s ease infinite;
}

@keyframes gradientShift {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}

.border-svg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
}

.animated-border-path {
  stroke-dasharray: 200;
  stroke-dashoffset: 200;
  animation: drawBorder 4s ease-in-out infinite;
}

@keyframes drawBorder {
  0% { stroke-dashoffset: 200; }
  50% { stroke-dashoffset: 0; }
  100% { stroke-dashoffset: -200; }
}

/* Glass Container */
.glass-container {
  position: relative;
  background: rgba(255, 255, 255, 0.03);
  backdrop-filter: blur(20px);
  border-radius: 21px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  overflow: hidden;
  z-index: 2;
}

.glass-container::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 1px;
  background: linear-gradient(90deg, 
    transparent, 
    rgba(255, 255, 255, 0.3), 
    transparent);
  animation: shimmer 3s ease-in-out infinite;
}

@keyframes shimmer {
  0%, 100% { opacity: 0; }
  50% { opacity: 1; }
}

/* Content Grid */
.content-grid {
  display: grid;
  grid-template-columns: 1.2fr 0.8fr;
  gap: 3rem;
  padding: 3rem;
  min-height: 500px;
}

.desc-section,
.accounts-section {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.desc-section.animate-in,
.accounts-section.animate-in {
  opacity: 1;
  transform: translateY(0);
}

.accounts-section.animate-in {
  transition-delay: 0.2s;
}

.fab:hover {
  transform: scale(1.1) rotate(10deg);
  box-shadow: 0 12px 40px rgba(255, 0, 110, 0.4);
}

.fab.spin {
  animation: spin 0.6s ease-in-out;
}

@keyframes spin {
  100% { transform: rotate(360deg); }
}

.fab-icon {
  width: 24px;
  height: 24px;
  color: white;
}

/* Icon transitions */
.icon-fade-enter-active,
.icon-fade-leave-active {
  transition: all 0.3s ease;
}

.icon-fade-enter-from {
  opacity: 0;
  transform: rotate(-180deg) scale(0.5);
}

.icon-fade-leave-to {
  opacity: 0;
  transform: rotate(180deg) scale(0.5);
}

/* Particles */
.particles-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 5;
}

.particle {
  position: absolute;
  width: 2px;
  height: 2px;
  background: radial-gradient(circle, white, transparent);
  border-radius: 50%;
  animation: particleFloat 5s linear infinite;
  bottom: -10px;
}

@keyframes particleFloat {
  0% {
    transform: translateY(100vh) rotate(0deg);
    opacity: 0;
  }
  10% {
    opacity: 1;
  }
  90% {
    opacity: 1;
  }
  100% {
    transform: translateY(-100px) rotate(360deg);
    opacity: 0;
  }
}

/* Responsive Design */
@media (max-width: 1024px) {
  .content-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
    padding: 2rem;
  }
  
  .fab {
    top: 1rem;
    right: 1rem;
    width: 48px;
    height: 48px;
  }
}

@media (max-width: 768px) {
  .presentation-section {
    padding: 1rem;
  }
  
  .content-grid {
    padding: 1.5rem;
  }
  
  .orb {
    display: none; /* Hide orbs on mobile for performance */
  }
}

/* Accessibility */
@media (prefers-reduced-motion: reduce) {
  .orb,
  .gradient-waves,
  .grid-overlay,
  .particle {
    animation: none;
  }
  
  .presentation-container {
    opacity: 1;
    transform: none;
  }
}
</style>