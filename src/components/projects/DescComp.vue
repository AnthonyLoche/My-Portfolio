<script setup>
import { ref, onMounted } from 'vue';
import router from "@/router";

// Props para o projeto
const props = defineProps({
    projeto: Object
});

const isVisible = ref(false);
const tagContainer = ref(null);

const openSrc = (src) => {
    window.open(src, '_blank');
};

const navigateToProject = () => {
    router.push(`/projeto/${props.projeto.nome}`);
};

onMounted(() => {
    setTimeout(() => {
        isVisible.value = true;
    }, 300);
});
</script>

<template>
    <section class="project-description" :class="{ 'visible': isVisible }">
        <div class="content-overlay">
            <div class="container">
                <!-- Tags Section -->
                <div class="tags-section" ref="tagContainer">
                    <div class="tags-wrapper">
                        <div 
                            v-for="(tag, index) in projeto.tags" 
                            :key="index" 
                            class="tag"
                            :style="{ animationDelay: `${index * 0.1}s` }"
                        >
                            <span class="tag-icon">#</span>
                            <span class="tag-text">{{ tag }}</span>
                        </div>
                    </div>
                </div>

                <!-- Project Info -->
                <div class="project-info">
                    <h2 class="project-title">{{ projeto.nome }}</h2>
                    <div class="project-description-text">
                        {{ projeto.descricao }}
                    </div>
                </div>

                <!-- Action Buttons -->
                <div class="action-buttons">
                    <button 
                        class="btn btn-primary"
                        @click="navigateToProject"
                    >
                        <svg class="btn-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor">
                            <path d="M2 12s3-7 10-7 10 7 10 7-3 7-10 7-10-7-10-7z"/>
                            <circle cx="12" cy="12" r="3"/>
                        </svg>
                        <span>Ver Detalhes</span>
                        <div class="btn-hover-effect"></div>
                    </button>
                    
                    <button 
                        class="btn btn-secondary"
                        @click="openSrc(projeto.src)"
                    >
                        <svg class="btn-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor">
                            <path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"/>
                        </svg>
                        <span>Código Fonte</span>
                        <div class="btn-hover-effect"></div>
                    </button>
                </div>
            </div>
        </div>
        
        <!-- Decorative Elements -->
        <div class="decorative-elements">
            <div class="floating-dot dot-1"></div>
            <div class="floating-dot dot-2"></div>
            <div class="floating-dot dot-3"></div>
        </div>
    </section>
</template>

<style scoped>
.project-description {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 10;
    transform: translateY(20px);
    opacity: 0;
    transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}

.project-description.visible {
    transform: translateY(0);
    opacity: 1;
}

.content-overlay {
    background: linear-gradient(
        180deg,
        rgba(0, 0, 0, 0) 0%,
        rgba(0, 0, 0, 0.4) 30%,
        rgba(0, 0, 0, 0.8) 70%,
        rgba(0, 0, 0, 0.95) 100%
    );
    backdrop-filter: blur(10px);
    padding: 3rem 2rem 2rem;
    border-radius: 0 0 16px 16px;
    position: relative;
}

.container {
    max-width: 800px;
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
}

.tags-section {
    margin-bottom: 0.5rem;
}

.tags-wrapper {
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem;
    align-items: center;
}

.tag {
    background: linear-gradient(135deg, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0.05));
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.2);
    padding: 0.5rem 1rem;
    border-radius: 25px;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    color: white;
    font-size: 0.85rem;
    font-weight: 500;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    opacity: 0;
    transform: translateY(10px);
    animation: tagSlideIn 0.6s cubic-bezier(0.4, 0, 0.2, 1) forwards;
    cursor: pointer;
    position: relative;
    overflow: hidden;
}

.tag::before {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
    transition: left 0.5s;
}

.tag:hover::before {
    left: 100%;
}

.tag:hover {
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(255, 255, 255, 0.1);
    border-color: rgba(255, 255, 255, 0.4);
}

.tag-icon {
    color: rgba(255, 255, 255, 0.7);
    font-weight: 600;
    font-size: 0.9rem;
}

.tag-text {
    font-weight: 500;
}

@keyframes tagSlideIn {
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.project-info {
    margin-bottom: 1rem;
}

.project-title {
    font-size: clamp(1.8rem, 4vw, 2.5rem);
    font-weight: 700;
    color: white;
    margin-bottom: 1rem;
    background: linear-gradient(135deg, #ffffff, #f0f0f0);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    line-height: 1.2;
    text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
}

.project-description-text {
    color: rgba(255, 255, 255, 0.9);
    font-size: 1.1rem;
    line-height: 1.6;
    font-weight: 400;
    max-width: 600px;
    text-shadow: 0 1px 3px rgba(0, 0, 0, 0.5);
}

.action-buttons {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
}

.btn {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    padding: 1rem 1.5rem;
    border: none;
    border-radius: 12px;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    position: relative;
    overflow: hidden;
    backdrop-filter: blur(10px);
    text-decoration: none;
    min-width: 160px;
    justify-content: center;
}

.btn-primary {
  background: linear-gradient(90deg, #d40c0c, #8b0000);
    color: white;
    box-shadow: 0 4px 15px rgba(255, 0, 120, 0.4);
    border: 1px solid rgba(255, 255, 255, 0.1);
}

.btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(255, 0, 120, 0.6);
  background: linear-gradient(90deg, #dc0a0a, #940202);
}

.btn-secondary {
    background: rgba(255, 255, 255, 0.1);
    color: white;
    border: 1px solid rgba(255, 255, 255, 0.3);
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
}

.btn-secondary:hover {
    transform: translateY(-2px);
    background: rgba(255, 255, 255, 0.2);
    border-color: rgba(255, 255, 255, 0.5);
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
}

.btn-icon {
    width: 20px;
    height: 20px;
    stroke-width: 2;
    transition: transform 0.3s ease;
}

.btn:hover .btn-icon {
    transform: scale(1.1);
}

.btn-hover-effect {
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
    transition: left 0.5s;
    pointer-events: none;
}

.btn:hover .btn-hover-effect {
    left: 100%;
}

.decorative-elements {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    pointer-events: none;
}

.floating-dot {
    position: absolute;
    width: 4px;
    height: 4px;
    background: rgba(255, 255, 255, 0.3);
    border-radius: 50%;
    animation: float 3s ease-in-out infinite;
}

.dot-1 {
    top: 20%;
    right: 10%;
    animation-delay: 0s;
}

.dot-2 {
    top: 60%;
    right: 20%;
    animation-delay: 1s;
}

.dot-3 {
    top: 40%;
    right: 5%;
    animation-delay: 2s;
}

@keyframes float {
    0%, 100% { 
        transform: translateY(0px); 
        opacity: 0.3;
    }
    50% { 
        transform: translateY(-10px); 
        opacity: 0.8;
    }
}

@media (max-width: 768px) {
    .content-overlay {
        padding: 2rem 1.5rem 1.5rem;
    }
    
    .container {
        gap: 1rem;
    }
    
    .project-title {
        font-size: 1.8rem;
        margin-bottom: 0.75rem;
    }
    
    .project-description-text {
        font-size: 1rem;
        line-height: 1.5;
    }
    
    .action-buttons {
        flex-direction: column;
        gap: 0.75rem;
    }
    
    .btn {
        padding: 0.875rem 1.25rem;
        font-size: 0.95rem;
        min-width: auto;
        width: 100%;
    }
    
    .tags-wrapper {
        gap: 0.5rem;
    }
    
    .tag {
        padding: 0.4rem 0.8rem;
        font-size: 0.8rem;
    }
}

@media (max-width: 480px) {
    .content-overlay {
        padding: 1.5rem 1rem 1rem;
    }
    
    .project-title {
        font-size: 1.5rem;
    }
    
    .project-description-text {
        font-size: 0.9rem;
    }
    
    .btn {
        padding: 0.75rem 1rem;
        font-size: 0.9rem;
    }
    
    .btn-icon {
        width: 18px;
        height: 18px;
    }
}
</style>