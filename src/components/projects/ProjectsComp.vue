<script setup>
import DescComp from './DescComp.vue';
import 'vue3-carousel/dist/carousel.css';
import { Carousel, Slide, Navigation } from 'vue3-carousel';

const projetos = [
    {
        nome: 'Fábrica Hackathon',
        imagem: 'https://w7.pngwing.com/pngs/50/791/png-transparent-daffy-duck-graphics.png',
        descricao: 'Descrição detalhada do Projeto 1.',
        tags: ['Django', 'Vue.js', 'CSS', "RabbitMQ", "Celery"],
        src: "https://github.com"
    },
    {
        nome: 'Fex Company',
        imagem: 'https://w7.pngwing.com/pngs/50/791/png-transparent-daffy-duck-graphics.png',
        descricao: 'Descrição detalhada do Projeto 2.',
        tags: ['Vue.js', 'SCSS', 'Django', 'Celery', 'RabbitMQ', "API PIX"],
        src: "https://github.com"
    },
    {
        nome: 'Fábrica Door',
        imagem: 'https://w7.pngwing.com/pngs/50/791/png-transparent-daffy-duck-graphics.png',
        descricao: 'Descrição detalhada do Projeto 3.',
        tags: ['Node.js', 'Postgres', 'Vue.js', 'CSS', "ESP32"],
        src: "https://github.com"


    },
    {
        nome: 'Fábrica Needs',
        imagem: 'https://w7.pngwing.com/pngs/50/791/png-transparent-daffy-duck-graphics.png',
        descricao: 'Descrição detalhada do Projeto 3.',
        tags: ['Vue.js', 'Django', 'CSS', "API PIX", "Node.js"],
        src: "https://github.com"
    },
];

const config = {
    autoplay: 5000,
    pauseAutoplayOnHover: true,
};
</script>

<template>
    <section class="main-section">
        <div class="animated-container">
            <div class="container">
                <h1 class="title-gradient">&lt;Projetos/&gt;</h1>
                <Carousel v-bind="config">
                    <Slide v-for="(projeto, index) in projetos" :key="index">
                        <div class="carousel__item">
                            <div class="allItem" :style="{ backgroundImage: `url('${projeto.imagem}')` }">
                                <DescComp :projeto="projeto" />
                            </div>
                        </div>
                    </Slide>
                    <template #addons>
                        <Navigation />
                    </template>
                </Carousel>
            </div>
        </div>
    </section>
</template>

<style scoped>
.main-section {
    width: 100%;
    position: relative;
}

.animated-container {
    position: relative;
    width: 100%;
    overflow: hidden;
}

h1 {
    margin-bottom: .5rem;
    font-size: 2.5rem;
}

.container {
    width: 80%;
    margin: auto;
    height: 25vw;
    position: relative;
    z-index: 2;
    background-color: rgba(28, 28, 28, 0.9);
    border-radius: 15px;
    padding: 30px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
    border: 5px solid transparent;
    /* Define a borda inicial */
}

/* Animação da linha correndo pela borda */
@keyframes borderMove {
    0% {
        border-left-color: red;
        border-top-color: transparent;
        border-right-color: transparent;
        border-bottom-color: transparent;
    }

    25% {
        border-left-color: transparent;
        border-top-color: red;
        border-right-color: transparent;
        border-bottom-color: transparent;
    }

    50% {
        border-left-color: transparent;
        border-top-color: transparent;
        border-right-color: red;
        border-bottom-color: transparent;
    }

    75% {
        border-left-color: transparent;
        border-top-color: transparent;
        border-right-color: transparent;
        border-bottom-color: red;
    }

    100% {
        border-left-color: red;
        border-top-color: transparent;
        border-right-color: transparent;
        border-bottom-color: transparent;
    }
}

.container {
    animation: borderMove 4s infinite linear;
    /* Aplica a animação à borda */
}

.carousel__item {
    height: 20vw;
    width: 100%;
    color: #fff;
    font-size: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.allItem {
    display: flex;
    align-items: center;
    width: 100%;
    height: 100%;
    background-size: cover;
    position: relative;
    object-fit: cover;
    border-radius: 10px;
}

.allItem::after {
    content: "";
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 10%;
    background: linear-gradient(to top, #131316, rgba(19, 19, 22, 0));
    z-index: 1;
}

.carousel__pagination {
    list-style: none !important;
}

.carousel__pagination-item {
    margin-top: 0 !important;
}

.carousel__slide {
    margin-top: 0 !important;
}

@media (max-width: 768px) {
    .container {
        grid-template-columns: 100%;
        width: 90%;
    }
}
</style>
