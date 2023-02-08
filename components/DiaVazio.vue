<template>
  <div :id="diasVazios1.id" class="diaEmBranco"></div>
</template>

<script>
export default {

}
</script>

<style scoped>
.diaEmBranco {
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

    background-color: #D9E5DF;
}
</style>