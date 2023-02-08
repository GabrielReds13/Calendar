<template>
  <div class="container">
    <div id="eventosRecentes">
      
    </div>
    <Mes />
    <!-- Trocar mes -->
  </div>

</template>

<script lang="ts">
  import Mes from './components/Mes.vue';
  export default {
    components: {
      Mes
    }  
  }
</script>

<style scoped>
  /* Geral */
  .container {
    display: flex;
    flex-direction: column;

    width: 100vw;
    height: 100vh;

    justify-content: center;
    align-items: center;
  }
</style>
