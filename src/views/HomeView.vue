<template>
  <BannerTest/>
  <div class="main-container">
    <h1>Monte sua pizza:</h1>
    <PizzaForm/>
  </div>
</template>

<script>
import BannerTest from "../components/BannerTest.vue"
import PizzaForm from "../components/PizzaForm.vue"

export default {
  name: "HomeView",
  components: {BannerTest, PizzaForm}
}
</script>
