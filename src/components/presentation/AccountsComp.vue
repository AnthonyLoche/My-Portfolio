<template>
  <div class="accounts-container">
    <h2 class="accounts-title">Redes Sociais</h2>
    <!-- Lista de redes sociais -->
    <ul class="social-list">
      <li v-for="social in socialNetworks" :key="social.name" class="social-item">
        <a :href="social.link" target="_blank" class="social-link">
          <span class="social-icon">
            <component :is="social.icon" />
          </span>
          <span class="social-name">{{ social.name }}</span>
        </a>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Linkedin from "vue-material-design-icons/Linkedin.vue"
import Instagram from "vue-material-design-icons/Instagram.vue"
import Twitter from "vue-material-design-icons/Twitter.vue"
import GitHub from "vue-material-design-icons/Github.vue"

const socialNetworks = ref([
  { name: 'Instagram', icon: GitHub, link: 'https://github.com' },
  { name: 'Instagram', icon: Instagram, link: 'https://instagram.com' },
  { name: 'Twitter', icon: Twitter, link: 'https://twitter.com' },
  { name: 'LinkedIn', icon: Linkedin, link: 'https://linkedin.com' },
])
</script>

<style scoped>
.accounts-container {
  max-width: 100%;
  padding: 1rem;
  text-align: left;
}

.accounts-title {
  font-size: 2.5rem;
  font-weight: bold;
  margin-bottom: 2rem;
  color: #8b0000;
}

label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

textarea {
  width: 100%;
  margin-bottom: 1rem;
  padding: 0.5rem;
  font-size: 1rem;
  resize: vertical;
}

ul {
  list-style-type: disc;
  margin-left: 1.5rem;
  margin-bottom: 1.5rem;
  padding: 0;
}

.social-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.social-item {
  margin-bottom: 1.5rem;
  transition: transform 0.3s ease;
  border-bottom: 1px solid #d40c0c;
  padding-bottom: .5rem;
}

.social-item:hover {
  transform: translateX(10px);
}

.social-link {
  display: flex;
  align-items: center;
  text-decoration: none;
  color: white;
  font-size: 1.25rem;
}

.social-icon {
  margin-right: 15px;
  font-size: 1.5rem;
  color: #d40c0c;
}

.social-name {
  font-weight: 600;
}
</style>
