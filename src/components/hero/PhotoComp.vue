<script setup>
</script>

<template>
    <div class="container">
        <div class="trapezoid"></div>
    </div>
</template>

<style scoped>
.container {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: transparent;
}

.trapezoid {
    width: 700px;
    height: 600px;
    background: url("./public/s.jpeg") no-repeat center;
    background-size: cover;
    clip-path: polygon(10% 0%, 70% 0%, 100% 60%, 0% 100%);
    animation: float 3s ease-in-out infinite alternate;

    box-shadow: 0 0 20px rgba(255, 255, 255, 0.4),
        0 0 40px rgba(255, 255, 255, 0.3),
        0 0 60px rgba(255, 255, 255, 0.2);
    transition: box-shadow 0.3s ease-in-out;
}

@keyframes float {
    0% {
        transform: translateY(-15px);
    }

    100% {
        transform: translateY(15px);
    }
}
</style>
