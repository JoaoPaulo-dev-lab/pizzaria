<template>
   <div id="nav">
    <router-link to="/" id="logo-url">
        <img :src="logo" :alt="alt"  id="logo">
    </router-link>
    <router-link class="home" to="/">Home</router-link> 
    <router-link class="pedidos" to="/pedidosview">Pedidos</router-link>
   </div>
</template>

<script>
export default {
    name: "NavbarTest", 
    props: ["logo", "alt"]
}
</script>

<style scoped>
    #nav {
        background-color: rgb(0, 87, 0);
        border-bottom: 4px solid rgb(0, 44, 0);
        padding: 15px 50px;
        display: flex;
        justify-content: flex-end;
        align-items: center;
    }

    #nav #logo-url {
        margin: auto;
        margin-left: 0;
    }

    #logo {
        width: 50px;
        height: 50px;
    }

    #nav a {
        color: #fff;
        text-decoration: none;
        margin: 12px;
        transition: .5s;

    }

    #nav a:hover {
        color: red;
    }

    .home,
    .pedidos {
        font-weight: bold;
    }
</style>