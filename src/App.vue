<template>
  <NavbarTest :logo="logo_src" :alt="app_name"/>
  <router-view/>
  <FooterTest/>
</template>

<script>
import NavbarTest from './components/NavbarTest.vue';
import FooterTest from './components/FooterTest.vue';

export default {
  components: {
    NavbarTest,
    FooterTest
  },
  data() {
    return {
    logo_src: "../img/pizzalogo.png",
    app_name: "Faça sua Pizza"
    }
  }
}

</script>

<style>
  * {
    font-family: Helvetica;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  .main-container{
    margin: 50px;
    min-height: 250px;
  }

  h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
  }
</style>
