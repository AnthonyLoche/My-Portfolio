<script setup>
import PhotoComp from './PhotoComp.vue';
import TextComp from './TextComp.vue';
</script>

<template>
    <div class="container">
        <div class="content">
            <PhotoComp />
            <TextComp />
        </div>
    </div>
</template>

<style scoped>
.container {
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}

.content {
    display: grid;
    grid-template-columns: 50% 50%; /* Cada componente ocupa 50% */
    width: 90%;
    gap: 10px; /* Espaço entre os componentes */
}

.content > * {
    width: 100%; /* Garantir que cada componente ocupe 100% do espaço de sua célula */
}

@media (max-width: 768px) {
    .content {
        grid-template-columns: 1fr; /* Quando a tela for pequena, os componentes ficam em coluna */
        align-items: center;
    }
}
</style>
