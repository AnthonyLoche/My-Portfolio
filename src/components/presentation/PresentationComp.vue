<script setup>
import DescComp from './DescComp.vue';
import AccountsComp from './AccountsComp.vue';
</script>

<template>
  <section class="main-section">
    <div class="animated-container">
      <div class="container">
        <DescComp />
        <AccountsComp />
      </div>
      <div class="animated-border"></div>
    </div>
  </section>
</template>

<style scoped>
.main-section {
  width: 100%;
  position: relative;
  padding: 40px 0;
}

.animated-container {
  position: relative;
  width: 100%;
  overflow: hidden;
}

.container {
  width: 80%;
  margin: 10px auto;
  display: grid;
  grid-template-columns: 60% 40%;
  position: relative;
  z-index: 2;
  background-color: rgba(28, 28, 28, 0.9);
  border-radius: 15px;
  padding: 30px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
}

.animated-border {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  border: 5px solid transparent;
  border-radius: 15px;
  background: radial-gradient(circle, rgba(255, 0, 0, 0.5) 10%, transparent 30%) top left,
              radial-gradient(circle, rgba(255, 0, 0, 0.5) 10%, transparent 30%) top right,
              radial-gradient(circle, rgba(255, 0, 0, 0.5) 10%, transparent 30%) bottom left,
              radial-gradient(circle, rgba(255, 0, 0, 0.5) 10%, transparent 30%) bottom right;
  background-size: 50% 50%;
  background-repeat: no-repeat;
  animation: borderEffect 3s linear infinite;
  z-index: 1;
}

@keyframes borderEffect {
  0%, 100% {
    background-position: top left, top right, bottom left, bottom right;
  }
  50% {
    background-position: top right, bottom right, bottom left, top left;
  }
}

@media (max-width: 768px) {
  .container {
    grid-template-columns: 100%;
    width: 90%;
  }
}
</style>
