<script setup>
import router from "@/router";

// Props para o projeto
defineProps({
    projeto: Object
});

const openSrc = (src) => {
    window.open(src, '_blank');
};

</script>


<template>
    <section>
        <div class="container">
            <div class="tags">
                <!-- Exibindo as tags dinamicamente a partir do array -->
                <div v-for="(tag, index) in projeto.tags" :key="index" class="tag">
                    {{ tag }}
                </div>
            </div>
            <h2>{{ projeto.nome }}</h2>
            <div class="desc">{{ projeto.descricao }}</div>
            <div class="buttons">
                <button class="green" @click="router.push(`/projeto/${projeto.nome}`)">
                    Ver Detalhes
                </button>
                <button class="black" @click="openSrc(projeto.src)">
                    Ver SRC
                </button>
            </div>
        </div>
    </section>
</template>

<style scoped>
section {
    width: 100%;
    margin: 0;
    padding: 20px;
    /* Ajusta o padding para evitar que o conteúdo encoste nas bordas */
    position: fixed;
    bottom: 0;
    left: 0;
    z-index: 10;
}

section::after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    /* Garante que a sombra ocupe toda a largura da tela */
    height: 100%;
    /* Ocupa toda a altura da section */
    background-color: rgba(0, 0, 0, 0.3);
    /* Fundo preto com opacidade */
    z-index: -1;
    filter: blur(5px);
    /* Suaviza o efeito de fundo */
}

.container {
    width: 50%;
    display: flex;
    flex-direction: column;
    align-items: start;
}

.tags {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
}

.tag {
    background-color: #070707;
    padding: 5px 10px;
    border-radius: 20px;
    display: inline-block;
    color: white;
    font-size: 10pt;
}

h2 {
    font-size: 30pt;
}

.desc {
    display: flex;
    align-items: start;
    font-size: 11pt;
    text-align: left;
}

.buttons {
    display: flex;
    align-items: center;
    margin-top: 20px;
    gap: 20px;
}

button {
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
}

.green {
    background-color: #d40c0c;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    transition: 0.5s ease-in-out;
}

.green:hover {
    background-color: #c41414;
}

.black {
    background-color: #161616;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    transition: 0.5s ease-in-out;
}

.black:hover {
    background-color: #191818;
}
</style>
