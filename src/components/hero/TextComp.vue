<script setup>
import { ref, onMounted } from 'vue';

const getGreeting = () => {
    const hours = new Date().getHours();
    if (hours < 12) {
        return 'Bom Dia';
    } else if (hours < 18) {
        return 'Boa Tarde';
    } else {
        return 'Boa Noite';
    }
};

const greeting = ref('');

onMounted(() => {
    greeting.value = getGreeting();
});
</script>

<template>
    <div class="welcome-container">
        <div class="space">
            <h1 class="welcome-title">
                <span class="title-gradient">{{ greeting }} </span>
                <span class="title-gradient">Seja Bem Vindo</span>
                <span class="title-gradient">Ao Meu Portfólio</span>
            </h1>
            <p class="welcome-text">
                Is simply dummy text of the printing and typesetting industry. Lorem Ipsum
                has been the industry's standard dummy text ever since the 1500s, when an
                unknown printer
            </p>
        </div>
    </div>
</template>

<style scoped>
.welcome-container {
    max-width: 600px;
    padding: 2rem;
    text-align: left;
    display: flex;
    align-items: center;
}

.welcome-title {
    font-size: 4rem;
    font-weight: bold;
    margin-bottom: 2rem;
    line-height: 1.2;
    display: flex;
    flex-direction: column;
}

.title-gradient {
    background: linear-gradient(90deg, #d40c0c, #8b0000, #2e2e2e, #1c1c1c);
    /* Novas cores de gradiente */
    background-size: 300% 300%;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    animation: gradientMove 3s infinite alternate;
}

@keyframes gradientMove {
    0% {
        background-position: 0%;
    }

    100% {
        background-position: 100%;
    }
}

.welcome-text {
    font-size: 1.25rem;
    line-height: 1.8;
    color: white;
    max-width: 600px;
    margin: 0 auto;
}

@media (max-width: 768px) {
    .welcome-title {
        font-size: 2.5rem;
    }
}
</style>
