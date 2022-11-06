<template>
    <div id="main-banner">
        <h1>Peça Sua Pizza</h1>
    </div>
</template>

<script>
export default {
    name: 'BannerTest'    
}
</script>

<style scoped>
    #main-banner {
        background-image: url('../assets/pizzaimg.jpg');
        background-size: cover; /* Imagem aparecendo o máximo possível no espaço */
        height: 500px;
        display: flex;
        align-items: center; /*Alinha o texto do banner a esquerda */
        justify-content: flex-start;
    }

    #main-banner h1 {
        color: #fff;
        text-align: center;
        font-size: 60px;
        background-color: rgba(0, 47, 0, 0.589);
        padding: 20px 40px;
    }
</style>