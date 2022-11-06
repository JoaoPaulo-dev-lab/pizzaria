<template>
  <div class="main-container">
    <h1 id="pedidos">Gerenciar pedidos:</h1>
    <Dashboard/>
  </div>
</template>

<script>
import Dashboard from "../components/Dashboard.vue"
export default {
  name: "PedidosView",
  components: { Dashboard }
}
</script>

<style scoped>
  #pedidos {
    color: rgb(0, 48, 0);
  }
</style>
