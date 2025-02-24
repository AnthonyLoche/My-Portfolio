<script setup>
import Home from "vue-material-design-icons/Home.vue";
import BriefcaseOutline from "vue-material-design-icons/BriefcaseOutline.vue";
import WebBox from "vue-material-design-icons/WebBox.vue";
import Email from "vue-material-design-icons/Email.vue";
</script>

<template>
    <div class="container">
        <header>
            <router-link to="/">
                <Home />
                Home
            </router-link>
            <router-link to="/">
                <BriefcaseOutline />
                Projetos
            </router-link>
            <router-link to="/">
                <WebBox />
                Tecnologias
            </router-link>
            <router-link to="/">
                <Email />
                Contato
            </router-link>
        </header>
    </div>
</template>

<style scoped>
header {
    width: 50%;
    margin: 0.5rem auto;
    padding: 1rem;
    background-color: #161616;
    border-radius: 50px;
    box-shadow: 0 2px 15px rgba(255, 255, 255, 0.1);
    text-align: center;
    font-size: 1.5rem;
    font-weight: bold;
    color: #fff;
    display: flex;
    justify-content: space-around;
    transition: box-shadow 0.3s ease-in-out;
    position: fixed;
    top: 10px;
    left: 25%;
    z-index: 100 !important;
}

header:hover {
    box-shadow: 0 0 20px rgba(255, 255, 255, 0.2);
}

header a {
    text-decoration: none;
    color: #fff;
    transition: text-shadow 0.3s ease-in-out;
    display: flex;
    gap: 0.5rem; 
}

span {
    display: flex;
    align-items: center;
    justify-content: center;
}
</style>
