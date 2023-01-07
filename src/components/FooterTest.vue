<template>
    <footer id="footer">
        <p>Peça sua Pizza &copy; <span id="year"></span></p>
    </footer>
</template>

<script>
export default {
    name: "FooterTest",

    methods: {
        getFullYear() {
            const year = document.getElementById('year')
            const anoAtual = new Date();
            year.innerHTML = anoAtual.getFullYear();
        }
    },
    mounted() {
        this.getFullYear()
    }
}
</script>

<style scoped>
    #footer {
        height: 130px;
        background-color: rgb(0, 87, 0);
        border-top: 4px solid rgb(0, 44, 0);
        color: #fff;
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100%;

    }
</style>