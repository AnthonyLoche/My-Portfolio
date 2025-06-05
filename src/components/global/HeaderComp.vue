<template>
  <nav class="navigation">
    <a
      v-for="item in navItems"
      :key="item.section"
      :href="`#${item.section}`"
      class="nav-item"
      :class="{ active: activeSection === item.section }"
      @click.prevent="setActive(item.section)"
    >
      <svg class="nav-icon" viewBox="0 0 24 24">
        <path :d="item.icon" />
      </svg>
      <span class="nav-text">{{ item.label }}</span>
    </a>
  </nav>
</template>

<script setup>
import { ref } from 'vue';

const navItems = [
  {
    label: 'Home',
    section: 'home',
    icon: 'M10,20V14H14V20H19V12H22L12,3L2,12H5V20H10Z',
  },
  {
    label: 'Projetos',
    section: 'projetos',
    icon: 'M12,2A10,10 0 0,0 2,12A10,10 0 0,0 12,22A10,10 0 0,0 22,12A10,10 0 0,0 12,2Z M12,4A8,8 0 0,1 20,12A8,8 0 0,1 12,20A8,8 0 0,1 4,12A8,8 0 0,1 12,4Z',
  },
  {
    label: 'Tecnologias',
    section: 'tecnologias',
    icon: 'M3,3H21V5H3V3M3,7H21V9H3V7M3,11H21V13H3V11M3,15H21V17H3V15M3,19H21V21H3V19Z',
  },
  {
    label: 'Contato',
    section: 'contato',
    icon: 'M20,8L12,13L4,8V6L12,11L20,6M20,4H4A2,2 0 0,0 2,6V18A2,2 0 0,0 4,20H20A2,2 0 0,0 22,18V6A2,2 0 0,0 20,4Z',
  },
];

const activeSection = ref('home');

function setActive(section) {
  activeSection.value = section;
}


</script>

<style scoped>
.navigation {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 25px;
  padding: 1.5rem;
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.3), inset 0 1px 0 rgba(255, 255, 255, 0.1);
  display: flex;
  gap: 1rem;
  justify-content: center;
  margin: auto;
  width: 40%;
  position: fixed;
  top: 10px;
  left: 30%;
  z-index: 100 !important;
}

.nav-item {
  position: relative;
  padding: 1rem 2rem;
  border-radius: 15px;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.05);
  color: rgba(255, 255, 255, 0.8);
  display: flex;
  align-items: center;
  gap: 0.75rem;
  text-decoration: none;
  transition: all 0.3s ease;
  cursor: pointer;
}

.nav-item:hover {
  background: rgba(255, 255, 255, 0.1);
  transform: scale(1.03);
  color: #fff;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3), 0 0 20px rgba(255, 255, 255, 0.1);
}

.nav-item.active {
  background: rgba(255, 255, 255, 0.15);
  color: #fff;
}

.nav-icon {
  width: 24px;
  height: 24px;
  fill: currentColor;
  transition: all 0.3s ease;
}

.nav-text {
  font-size: 0.95rem;
  font-weight: 600;
}
</style>
