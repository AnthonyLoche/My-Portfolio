<template>
    <div class="accounts-container">
      <h2 class="accounts-title">Redes Sociais</h2>
      <ul class="social-list">
        <li v-for="social in socialNetworks" :key="social.name" class="social-item">
          <a :href="social.link" target="_blank" class="social-link">
            <span class="social-icon">{{ social.icon }}</span>
            <span class="social-name">{{ social.name }}</span>
          </a>
        </li>
      </ul>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const socialNetworks = ref([
    { name: 'Instagram', icon: '📸', link: 'https://instagram.com' },
    { name: 'Facebook', icon: '👍', link: 'https://facebook.com' },
    { name: 'Twitter', icon: '🐦', link: 'https://twitter.com' },
    { name: 'LinkedIn', icon: '💼', link: 'https://linkedin.com' },
    { name: 'YouTube', icon: '▶️', link: 'https://youtube.com' }
  ]);
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
  }
  
  .social-name {
    font-weight: 600;
  }
  </style>