<template>
  <div class="desc-container" ref="containerRef">
    <!-- Animated Title -->
    <div class="title-section">
      <h1 class="main-title" :class="{ 'animate': isVisible }">
        <span class="title-char" 
              v-for="(char, index) in titleChars" 
              :key="index"
              :style="{ animationDelay: `${index * 0.1}s` }"
              :class="{ 'space': char === ' ' }">
          {{ char }}
        </span>
      </h1>
      
    </div>

    <!-- Content Section -->
    <div class="content-section" :class="{ 'fade-in': showContent }">
      <!-- Animated description -->
      <div class="text-container">
        <div class="description-text">
          Aprendiz de Desenvolvedor Full-Stack apaixonado por criar 
          experiências digitais extraordinárias. 
          Especializado em tecnologias modernas como 
          e sempre em busca de inovação e excelência.
        </div>
        
        <!-- Stats Cards -->
        <div class="stats-grid">
          <div class="stat-card" 
               v-for="(stat, index) in stats" 
               :key="stat.label"
               :style="{ animationDelay: `${index * 0.2}s` }"
               :class="{ 'visible': showStats }">
            <div class="stat-icon">
              <component :is="stat.icon" />
            </div>
            <div class="stat-content">
              <div class="stat-number">
                <AnimatedNumber :value="stat.value" :duration="2000" />
              </div>
              <div class="stat-label">{{ stat.label }}</div>
            </div>
          </div>
        </div>
      </div>

      <!-- Call to Action -->
      <div class="cta-section" :class="{ 'slide-up': showCTA }">
        <button class="cta-button primary" @click="scrollToProjects">
          <span class="cta-text">Ver Projetos</span>
          <div class="cta-icon">
            <ArrowIcon />
          </div>
          <div class="cta-ripple"></div>
        </button>
        
        <button class="cta-button secondary" @click="downloadCV">
          <span class="cta-text">Download CV</span>
          <div class="cta-icon">
            <DownloadIcon />
          </div>
        </button>
      </div>
    </div>

    <!-- Background Elements -->
    <div class="bg-elements">
      <div class="code-lines">
        <div v-for="n in 8" :key="n" class="code-line" :style="getCodeLineStyle(n)">
          <span class="line-number">{{ n.toString().padStart(2, '0') }}</span>
          <span class="line-content">{{ getCodeContent(n) }}</span>
        </div>
      </div>
      
      <div class="floating-shapes">
        <div class="shape triangle"></div>
        <div class="shape circle"></div>
        <div class="shape square"></div>
      </div>
    </div>
  </div>
</template>

<script setup>
import Console from "vue-material-design-icons/Console.vue"
import ProjectorScreenOutline from "vue-material-design-icons/ProjectorScreenOutline.vue"
import Numeric from "vue-material-design-icons/Numeric.vue"
import ArrowIcon from "vue-material-design-icons/ArrowRightBoldOutline.vue"
import DownloadIcon from "vue-material-design-icons/Download.vue"
import { ref, reactive, onMounted } from 'vue'

// Typed Text Component
// const TypedText = {
//   props: ['strings', 'loop', 'showCursor'],
//   setup(props) {
//     const currentText = ref('')
//     const currentIndex = ref(0)
//     const isDeleting = ref(false)
    
//     const typeText = () => {
//       const currentString = props.strings[currentIndex.value]
      
//       if (isDeleting.value) {
//         currentText.value = currentString.substring(0, currentText.value.length - 1)
//         if (currentText.value === '') {
//           isDeleting.value = false
//           currentIndex.value = (currentIndex.value + 1) % props.strings.length
//         }
//       } else {
//         currentText.value = currentString.substring(0, currentText.value.length + 1)
//         if (currentText.value === currentString) {
//           setTimeout(() => {
//             isDeleting.value = true
//           }, 2000)
//         }
//       }
      
//       const speed = isDeleting.value ? 50 : 100
//       setTimeout(typeText, speed)
//     }
    
//     onMounted(() => {
//       setTimeout(typeText, 1000)
//     })
    
//     return { currentText }
//   },
//   template: '<span class="typed-text">{{ currentText }}</span>'
// }

const AnimatedNumber = {
  props: ['value', 'duration'],
  setup(props) {
    const displayValue = ref(0)
    
    onMounted(() => {
      const startTime = Date.now()
      const animate = () => {
        const elapsed = Date.now() - startTime
        const progress = Math.min(elapsed / props.duration, 1)
        const easeOut = 1 - Math.pow(1 - progress, 3)
        
        displayValue.value = Math.floor(props.value * easeOut)
        
        if (progress < 1) {
          requestAnimationFrame(animate)
        }
      }
      
      setTimeout(() => requestAnimationFrame(animate), 500)
    })
    
    return { displayValue }
  },
  template: '<span>{{ displayValue }}</span>'
}

const containerRef = ref(null)
const isVisible = ref(false)
const showContent = ref(false)
const showStats = ref(false)
const showCTA = ref(false)
const showCursor = ref(true)

// Title animation
const title = '<Apresentação/>'
const titleChars = ref([...title])

const stats = reactive([
  {
    label: 'Projetos',
    value: 47,
    icon: ProjectorScreenOutline
  },
  {
    label: 'Tecnologias',
    value: 23,
    icon: Console
  },
  {
    label: 'Anos Exp.',
    value: 5,
    icon: Numeric
  }
])

const getCodeLineStyle = (n) => ({
  '--delay': `${n * 0.2}s`,
  '--offset': `${n * 10}px`
})

const getCodeContent = (n) => {
  const codeLines = [
    'const developer = {',
    '  name: "Anthony Gabriel",',
    '  skills: ["Vue", "React"],',
    '  passion: "Innovation",',
    '  location: "Brasil",',
    '  status: "Available",',
    '  coffee: true,',
    '};'
  ]
  return codeLines[n - 1] || ''
}

const scrollToProjects = () => {
  console.log('Scrolling to projects...')
}

const downloadCV = () => {
  console.log('Downloading CV...')
}

// Lifecycle
onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          isVisible.value = true
          setTimeout(() => showContent.value = true, 800)
          setTimeout(() => showStats.value = true, 1200)
          setTimeout(() => showCTA.value = true, 1600)
        }
      })
    },
    { threshold: 0.3 }
  )
  
  if (containerRef.value) {
    observer.observe(containerRef.value)
  }
  
  setInterval(() => {
    showCursor.value = !showCursor.value
  }, 800)
})
</script>

<style scoped>
.desc-container {
  position: relative;
  width: 100%;
  padding: 2rem 0;
  overflow: hidden;
}

/* Title Section */
.title-section {
  position: relative;
  margin-bottom: 2rem;
}

.main-title {
  font-size: clamp(2rem, 4vw, 4rem);
  font-weight: 800;
  line-height: 1.1;
  margin: 0;
  position: relative;
  font-family: 'SF Mono', 'Monaco', 'Cascadia Code', monospace;
}

.title-char {
  display: inline-block;
  opacity: 0;
  transform: translateY(50px) rotateX(90deg);
  animation: none;
  background: linear-gradient(90deg, #d40c0c, #8b0000, #2e2e2e, #1c1c1c);
  background-size: 400% 400%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  animation: gradientFlow 8s ease infinite;
}

.title-char.space {
  width: 0.3em;
}

.main-title.animate .title-char {
  animation: 
    charReveal 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94) forwards,
    gradientFlow 8s ease infinite;
}

@keyframes charReveal {
  to {
    opacity: 1;
    transform: translateY(0) rotateX(0);
  }
}

@keyframes gradientFlow {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}

.cursor {
  font-size: clamp(2.5rem, 5vw, 4.5rem);
  color: #06ffa5;
  opacity: 1;
  transition: opacity 0.1s ease;
  margin-left: 0.1em;
}

.cursor.blink {
  opacity: 0;
}

/* Content Section */
.content-section {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.content-section.fade-in {
  opacity: 1;
  transform: translateY(0);
}

.text-container {
  margin-bottom: 3rem;
}

.description-text {
  font-size: 1rem;
  line-height: 1.8;
  color: rgba(255, 255, 255, 0.9);
  margin-bottom: 2rem;
  font-weight: 400;
}

.text-highlight {
  background: linear-gradient(135deg, #d40c0c, #8b0000, #2e2e2e, #1c1c1c);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-weight: 700;
}

.text-accent {
  color: #d40c0c;
  font-weight: 600;
}

.tech-highlight {
  color: #3a86ff;
  font-weight: 700;
  font-family: 'SF Mono', monospace;
  padding: 0.2em 0.4em;
  background: rgba(58, 134, 255, 0.1);
  border-radius: 4px;
  border: 1px solid rgba(58, 134, 255, 0.2);
}

.typed-text {
  display: inline-block;
  min-width: 100px;
}

/* Stats Grid */
.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  gap: 1.5rem;
  margin: 2rem 0;
}

.stat-card {
  background: rgba(255, 255, 255, 0.03);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 16px;
  padding: 1.5rem;
  text-align: center;
  opacity: 0;
  transform: translateY(20px) scale(0.9);
  transition: all 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  position: relative;
  overflow: hidden;
}

.stat-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, 
    transparent, 
    rgba(255, 255, 255, 0.1), 
    transparent);
  transition: left 0.5s ease;
}

.stat-card:hover::before {
  left: 100%;
}

.stat-card.visible {
  opacity: 1;
  transform: translateY(0) scale(1);
}

.stat-card:hover {
  transform: translateY(-5px) scale(1.01);
  border-color: rgba(255, 255, 255, 0.2);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
}

.stat-icon {
  width: 40px;
  height: 40px;
  margin: 0 auto 1rem;
  color: #06ffa5;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(6, 255, 165, 0.1);
  border-radius: 12px;
  transition: all 0.3s ease;
}

.stat-card:hover .stat-icon {
  transform: scale(1.2) rotate(10deg);
  background: rgba(6, 255, 165, 0.2);
}

.stat-number {
  font-size: 2rem;
  font-weight: 800;
  color: white;
  margin-bottom: 0.5rem;
  font-family: 'SF Mono', monospace;
}

.stat-suffix {
  color: #ff006e;
  font-size: 1.5rem;
}

.stat-label {
  font-size: 0.875rem;
  color: rgba(255, 255, 255, 0.7);
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

/* CTA Section */
.cta-section {
  display: flex;
  gap: 1rem;
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.cta-section.slide-up {
  opacity: 1;
  transform: translateY(0);
}

.cta-button {
  position: relative;
  padding: 1rem 2rem;
  border: none;
  border-radius: 50px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  transition: all 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  overflow: hidden;
  text-decoration: none;
  font-family: inherit;
}

.cta-button.primary {
  background: linear-gradient(135deg, #2e2e2e,  #d40c0c, #8b0000);
  color: white;
}

.cta-button.secondary {
  background: rgba(255, 255, 255, 0.05);
  color: white;
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.cta-button:hover {
  transform: translateY(-3px);
}

.cta-button.secondary:hover {
  background: rgba(255, 255, 255, 0.1);
  border-color: rgba(255, 255, 255, 0.3);
}

.cta-icon {
  width: 20px;
  height: 20px;
  transition: transform 0.3s ease;
}

.cta-button:hover .cta-icon {
  transform: translateX(3px);
}

.cta-ripple {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 0;
  height: 0;
  background: rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  transform: translate(-50%, -50%);
  transition: all 0.3s ease;
}

.cta-button:active .cta-ripple {
  width: 200px;
  height: 200px;
}

/* Background Elements */
.bg-elements {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: -1;
  opacity: 0.3;
}

.code-lines {
  position: absolute;
  right: -20%;
  top: 10%;
  font-family: 'SF Mono', monospace;
  font-size: 0.875rem;
  transform: rotate(15deg);
}

.code-line {
  display: flex;
  align-items: center;
  margin-bottom: 0.5rem;
  opacity: 0;
  transform: translateX(var(--offset));
  animation: codeReveal 0.8s ease forwards;
  animation-delay: var(--delay);
}

@keyframes codeReveal {
  to {
    opacity: 0.6;
    transform: translateX(0);
  }
}

.line-number {
  color: rgba(255, 255, 255, 0.3);
  margin-right: 1rem;
  min-width: 24px;
}

.line-content {
  color: rgba(6, 255, 165, 0.6);
}

.floating-shapes {
  position: absolute;
  width: 100%;
  height: 100%;
}

.shape {
  position: absolute;
  opacity: 0.1;
}

.triangle {
  width: 60px;
  height: 60px;
  background: linear-gradient(135deg, #ff006e, transparent);
  clip-path: polygon(50% 0%, 0% 100%, 100% 100%);
  top: 20%;
  right: 10%;
  animation: float 6s ease-in-out infinite;
}

.circle {
  width: 80px;
  height: 80px;
  background: radial-gradient(circle, #3a86ff, transparent);
  border-radius: 50%;
  bottom: 30%;
  right: 5%;
  animation: float 8s ease-in-out infinite reverse;
}

.square {
  width: 40px;
  height: 40px;
  background: linear-gradient(45deg, #06ffa5, transparent);
  top: 60%;
  right: 20%;
  animation: float 7s ease-in-out infinite;
  transform: rotate(45deg);
}

span {
    display: flex;
    align-items: center;
    justify-content: center;
}

@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-20px); }
}

/* Responsive Design */
@media (max-width: 768px) {
  .desc-container {
    padding: 1rem 0;
  }
  
  .description-text {
    font-size: 1.1rem;
  }
  
  .stats-grid {
    grid-template-columns: repeat(3, 1fr);
    gap: 1rem;
  }
  
  .stat-card {
    padding: 1rem;
  }
  
  .stat-number {
    font-size: 1.5rem;
  }
  
  .cta-section {
    flex-direction: column;
  }
  
  .cta-button {
    justify-content: center;
  }
  
  .code-lines {
    display: none;
  }
}

/* Accessibility */
@media (prefers-reduced-motion: reduce) {
  .title-char,
  .stat-card,
  .cta-section,
  .code-line,
  .shape {
    animation: none;
    transition: none;
  }
  
  .main-title.animate .title-char {
    opacity: 1;
    transform: none;
  }
  
  .stat-card.visible {
    opacity: 1;
    transform: none;
  }
}
</style>