<template>
  <div id="nomeDoMes" class="nomeDoMes">
    <h3>{{ nomeDesteMes }}</h3>
  </div>
</template>

<script>
export default {
  name: "NomeDoMes",
  props: {
    nomeDesteMes: String
  }
}
</script>

<style scoped>
  /* Nome do mes */
  .nomeDoMes {
    display: flex;
    flex-direction: column;

    width: 90%;
    height: 10%;
    
    background-color: #90bda5;

    justify-content: center;
    align-items: center;

    border-radius: 25px;

    color: #fff;
  }
</style>>