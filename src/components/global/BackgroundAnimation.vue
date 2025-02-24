<template>
    <canvas ref="canvas" class="background"></canvas>
</template>

<script setup>
import { onMounted, ref } from "vue";

const canvas = ref(null);
let ctx, width, height;
const particles = [];

class Particle {
    constructor() {
        this.side = Math.random() > 0.5 ? "right" : "left";
        this.x = this.side === "right" ? width : 0;
        this.y = Math.random() * height;
        this.size = Math.random() * 3 + 1;
        this.speedX = this.side === "right" ? Math.random() * -2 - 1 : Math.random() * 2 + 1;
        this.speedY = Math.random() * 2 - 1;
    }

    update() {
        this.x += this.speedX;
        this.y += this.speedY;

        if (this.side === "right" && this.x < 0) {
            this.x = width;
            this.y = Math.random() * height;
        } else if (this.side === "left" && this.x > width) {
            this.x = 0;
            this.y = Math.random() * height;
        }
    }

    draw() {
        ctx.fillStyle = "#d40c0c";
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
        ctx.fill();
    }
}

function initParticles() {
    for (let i = 0; i < 50; i++) {
        particles.push(new Particle());
    }
}

function animate() {
    ctx.fillStyle = "#131316";
    ctx.fillRect(0, 0, width, height);

    particles.forEach((particle) => {
        particle.update();
        particle.draw();
    });

    requestAnimationFrame(animate);
}

onMounted(() => {
    canvas.value.width = width = window.innerWidth;
    canvas.value.height = height = window.innerHeight;
    ctx = canvas.value.getContext("2d");

    initParticles();
    animate();
});
</script>

<style scoped>
.background {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    z-index: -1;
}
</style>
