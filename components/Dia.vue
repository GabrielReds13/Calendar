<template>
  <div class="dia" :key="numeroDoDia">
    <h3 :id="numeroDoDia" class="numeroDoDia">{{ diaID }}</h3>
  </div>
</template>

<script>
export default {
  name: "Dia",
  props: {
    numeroDoDia: String,
    diaID: String,
  }
}
</script>

<style scoped>
.dia {
    display: flex;
    
    width: 8vh;
    min-width: 52px !important;
    height: 8vh;
    min-height: 52px !important;

    gap: 5% 5%;
    
    justify-content: center;
    align-items: center;
    
    padding: 0.3%;
    border-radius: 100%;

    background-color: #90bda5;
}

.numeroDoDia {
  display: flex;

  width: 82%;
  height: 82%;

  justify-content: center;
  align-items: center;

  border-radius: 100%;
  border: 2px solid #ffffff00;

  background-color: #90bda5;
  color: #fff !important;
}
.numeroDoDiaAtual {
  border: 2px solid #fff !important;
}
</style>