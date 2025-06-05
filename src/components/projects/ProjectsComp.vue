<script setup>
import DescComp from './DescComp.vue';
import 'vue3-carousel/dist/carousel.css';
import { Carousel, Slide, Navigation, Pagination } from 'vue3-carousel';
import { ref, onMounted } from 'vue';

const projetos = [
    {
        nome: 'Fábrica Hackathon',
        imagem: 'https://images.unsplash.com/photo-1581091226825-a6a2a5aee158?w=800&h=600&fit=crop',
        descricao: 'Plataforma inovadora para hackathons com sistema de colaboração em tempo real e avaliação automatizada.',
        tags: ['Django', 'Vue.js', 'CSS', "RabbitMQ", "Celery"],
        src: "https://github.com",
        categoria: "Web Development"
    },
    {
        nome: 'Fex Company',
        imagem: 'https://images.unsplash.com/photo-1460925895917-afdab827c52f?w=800&h=600&fit=crop',
        descricao: 'Sistema completo de gestão empresarial com integração PIX e automação de processos financeiros.',
        tags: ['Vue.js', 'SCSS', 'Django', 'Celery', 'RabbitMQ', "API PIX"],
        src: "https://github.com",
        categoria: "Fintech"
    },
    {
        nome: 'Fábrica Door',
        imagem: 'https://images.unsplash.com/photo-1558618047-3c8c76ca7d13?w=800&h=600&fit=crop',
        descricao: 'Controle inteligente de acesso com IoT, monitoramento em tempo real e integração com ESP32.',
        tags: ['Node.js', 'Postgres', 'Vue.js', 'CSS', "ESP32"],
        src: "https://github.com",
        categoria: "IoT"
    },
    {
        nome: 'Fábrica Needs',
        imagem: 'https://images.unsplash.com/photo-1551288049-bebda4e38f71?w=800&h=600&fit=crop',
        descricao: 'Marketplace inteligente para conectar necessidades locais com soluções personalizadas.',
        tags: ['Vue.js', 'Django', 'CSS', "API PIX", "Node.js"],
        src: "https://github.com",
        categoria: "E-commerce"
    },
];

const currentSlide = ref(0);
const isLoaded = ref(false);

const config = {
    autoplay: 6000,
    pauseAutoplayOnHover: true,
    transition: 800,
    wrapAround: true,
};

onMounted(() => {
    setTimeout(() => {
        isLoaded.value = true;
    }, 100);
});
</script>

<template>
    <section class="main-section" :class="{ 'loaded': isLoaded }">
        <div class="background-gradient"></div>
        <div class="floating-elements">
            <div class="floating-circle circle-1"></div>
            <div class="floating-circle circle-2"></div>
            <div class="floating-circle circle-3"></div>
        </div>
        
        <div class="animated-container">
            <div class="container">
                <div class="header-section">
                    <h1 class="title-gradient">
                        <span class="title-bracket">&lt;</span>
                        <span class="title-text">Projetos</span>
                        <span class="title-bracket">/&gt;</span>
                    </h1>
                    <div class="subtitle">Explore meus trabalhos mais recentes</div>
                </div>
                
                <div class="carousel-wrapper">
                    <Carousel 
                        v-bind="config" 
                        @slide-start="currentSlide = $event.currentSlideIndex"
                        class="custom-carousel"
                    >
                        <Slide v-for="(projeto, index) in projetos" :key="index">
                            <div class="carousel__item">
                                <div class="project-card" :style="{ backgroundImage: `url('${projeto.imagem}')` }">
                                    <div class="card-overlay"></div>
                                    <div class="category-badge">{{ projeto.categoria }}</div>
                                    <DescComp :projeto="projeto" />
                                </div>
                            </div>
                        </Slide>
                        <template #addons>
                            <Navigation />
                            <Pagination />
                        </template>
                    </Carousel>
                </div>
                
                <div class="progress-indicator">
                    <div class="progress-bar">
                        <div 
                            class="progress-fill" 
                            :style="{ width: `${((currentSlide + 1) / projetos.length) * 100}%` }"
                        ></div>
                    </div>
                    <span class="progress-text">{{ currentSlide + 1 }} / {{ projetos.length }}</span>
                </div>
            </div>
        </div>
    </section>
</template>

<style scoped>
.main-section {
    width: 100%;
    min-height: 100vh;
    position: relative;
    background: linear-gradient(135deg, #0c0c0c 0%, #1a1a1a 50%, #0f0f0f 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 2rem 0;
    opacity: 0;
    transform: translateY(30px);
    transition: all 1s cubic-bezier(0.4, 0, 0.2, 1);
}

.main-section.loaded {
    opacity: 1;
    transform: translateY(0);
}


.floating-elements {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    pointer-events: none;
    overflow: hidden;
}

.floating-circle {
    position: absolute;
    border-radius: 50%;
    background: linear-gradient(45deg, rgba(255, 0, 120, 0.1), rgba(120, 0, 255, 0.1));
    animation: float 20s infinite linear;
}

.circle-1 {
    width: 300px;
    height: 300px;
    top: 10%;
    left: -150px;
    animation-delay: 0s;
}

.circle-2 {
    width: 200px;
    height: 200px;
    top: 60%;
    right: -100px;
    animation-delay: -10s;
}

.circle-3 {
    width: 150px;
    height: 150px;
    bottom: 20%;
    left: 20%;
    animation-delay: -5s;
}

@keyframes float {
    0% { transform: translateY(0px) rotate(0deg); }
    33% { transform: translateY(-20px) rotate(120deg); }
    66% { transform: translateY(10px) rotate(240deg); }
    100% { transform: translateY(0px) rotate(360deg); }
}

.animated-container {
    position: relative;
    width: 100%;
    max-width: 1400px;
    margin: 0 auto;
    z-index: 2;
}

.container {
    width: 90%;
    margin: auto;
    position: relative;
    background: rgba(15, 15, 15, 0.8);
    backdrop-filter: blur(20px);
    border-radius: 24px;
    padding: 3rem;
    box-shadow: 
        0 20px 60px rgba(0, 0, 0, 0.4),
        0 0 0 1px rgba(255, 255, 255, 0.05),
        inset 0 1px 0 rgba(255, 255, 255, 0.1);
    border: 1px solid transparent;
    background-clip: padding-box;
    position: relative;
    overflow: hidden;
}

@keyframes borderRotate {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}

.header-section {
    text-align: center;
    margin-bottom: 3rem;
}

.title-gradient {
    font-size: clamp(2.5rem, 5vw, 4rem);
    margin-bottom: 1rem;
  background: linear-gradient(90deg, #d40c0c, #8b0000, #2e2e2e, #1c1c1c);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    display: inline-block;
    font-weight: 700;
    position: relative;
}

.title-bracket {
    color: rgba(255, 255, 255, 0.6);
    font-weight: 300;
}

.title-text {
    margin: 0 0.5rem;
    font-weight: 700;
    letter-spacing: -0.02em;
}

.subtitle {
    color: rgba(255, 255, 255, 0.7);
    font-size: 1.1rem;
    font-weight: 300;
}

.carousel-wrapper {
    margin-bottom: 2rem;
}

.carousel__item {
    height: 28vw;
    min-height: 400px;
    max-height: 600px;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 1rem;
}

.project-card {
    width: 100%;
    height: 100%;
    background-size: cover;
    background-position: center;
    border-radius: 16px;
    position: relative;
    overflow: hidden;
    transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
    box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
}

.project-card:hover {
    transform: scale(1.02);
    box-shadow: 0 20px 60px rgba(0, 0, 0, 0.5);
}

.card-overlay {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: linear-gradient(
        135deg,
        rgba(0, 0, 0, 0.3) 0%,
        rgba(0, 0, 0, 0.5) 50%,
        rgba(0, 0, 0, 0.8) 100%
    );
}

.category-badge {
    position: absolute;
    top: 1.5rem;
    right: 1.5rem;
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(10px);
    padding: 0.5rem 1rem;
    border-radius: 20px;
    color: white;
    font-size: 0.8rem;
    font-weight: 500;
    border: 1px solid rgba(255, 255, 255, 0.2);
    z-index: 3;
}

.progress-indicator {
    display: flex;
    align-items: center;
    gap: 1rem;
    justify-content: center;
}

.progress-bar {
    width: 200px;
    height: 4px;
    background: rgba(255, 255, 255, 0.1);
    border-radius: 2px;
    overflow: hidden;
}

.progress-fill {
    height: 100%;
  background: linear-gradient(90deg, #d40c0c, #8b0000);
    border-radius: 2px;
    transition: width 0.6s cubic-bezier(0.4, 0, 0.2, 1);
}

.progress-text {
    color: rgba(255, 255, 255, 0.7);
    font-size: 0.9rem;
    font-weight: 500;
}

/* Estilos do Carousel */
:deep(.carousel__prev),
:deep(.carousel__next) {
    background: rgba(255, 255, 255, 0.1) !important;
    backdrop-filter: blur(10px) !important;
    border: 1px solid rgba(255, 255, 255, 0.2) !important;
    color: white !important;
    width: 50px !important;
    height: 50px !important;
    border-radius: 50% !important;
    transition: all 0.3s ease !important;
}

:deep(.carousel__prev:hover),
:deep(.carousel__next:hover) {
    background: rgba(255, 255, 255, 0.2) !important;
    transform: scale(1.1) !important;
}

:deep(.carousel__pagination) {
    padding: 1rem 0 !important;
}

:deep(.carousel__pagination-button) {
    background: rgba(255, 255, 255, 0.3) !important;
    width: 12px !important;
    height: 12px !important;
    border-radius: 50% !important;
    margin: 0 0.3rem !important;
    transition: all 0.3s ease !important;
}

:deep(.carousel__pagination-button--active) {
    background: linear-gradient(90deg, #d40c0c, #8b0000) !important;
    transform: scale(1.2) !important;
}

@media (max-width: 768px) {
    .container {
        width: 95%;
        padding: 2rem 1.5rem;
    }
    
    .carousel__item {
        height: 60vw;
        min-height: 350px;
    }
    
    .title-gradient {
        font-size: 2.5rem;
    }
    
    .progress-bar {
        width: 150px;
    }
}

@media (max-width: 480px) {
    .container {
        padding: 1.5rem 1rem;
    }
    
    .carousel__item {
        height: 70vw;
        min-height: 300px;
    }
}</style>