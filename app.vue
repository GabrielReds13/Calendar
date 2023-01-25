<template>
  <div class="container">
    <!-- Calendario -->
    <div id="calendario">
      <div id="nomeDoMes" class="nomeDoMes">
        <h3>{{ mesAtual }}</h3>
      </div>

      <!-- Semana -->
      <div class="semana">
        <div v-for="semana in semanaItens" :key="semana.id">
            <h3>{{ semana.id }}</h3>
        </div>
      </div>

      <div class="diasDoMes">
        <!-- Dias do mes -->
        <div v-for="dias in totalDeDiasNoMes" :key="dias.id">
          <div class="dia">
            <h3 :id="dias.nomeDoItem" class="numeroDoDia">{{ dias.id }}</h3>
          </div>
        </div>
      </div>
    </div>

    <!-- Trocar mes -->
  </div>
</template>

<script lang="ts">
  import dayjs from 'dayjs';

  export default {
    data() {
      return {
        meses: new Array("Janeiro","Fevereiro","Marco","Abril","Maio","Junho","Julho","Agosto","Septembro","Outubro","Novembro","Dezembro"),
        semanaItens: new Array({id: "Dom"}, {id: "Seg"}, {id: "Ter"}, {id: "Qua"}, {id: "Qui"}, {id: "Sex"}, {id: "Sáb"}),
        mesAtual: "",
        totalDeDiasNoMes: [{id: "", nomeDoItem: ""}],

      }
    },
    methods: {
      async setarMes() {
        const pegarMesAtual = dayjs().startOf("month").toDate()
        const checarMesAtual = parseInt(dayjs(pegarMesAtual).format("MM"))
        this.mesAtual = this.meses[(checarMesAtual - 1)].toUpperCase()
      },
      async setarDiasNoMes() {
        const pegarDataAtual = dayjs().startOf("day").toDate()
        const checarMesAtual = dayjs(pegarDataAtual).format("YYYY-MM-DD")
        let diasNoMes = dayjs(`${checarMesAtual}`).daysInMonth()
        this.totalDeDiasNoMes.shift()
        for(let i = 1; i < (diasNoMes + 1); i++) {
          this.totalDeDiasNoMes.push({id: `${i}`, nomeDoItem: `itemN${i}`})
        }
        document.addEventListener("DOMContentLoaded", function () {
          document.getElementById(`itemN${dayjs(pegarDataAtual).format("DD")}`)?.classList.add("numeroDoDiaAtual")
        })
      }
    },
    mounted() {
      this.setarMes()
      this.setarDiasNoMes()
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

  /* Calendario */
  #calendario {
    display: flex;
    flex-direction: column;

    width: 33vw;/* 
    height: 75vh; */
    min-height: 500px;
    height: 70%;

    justify-content: space-evenly;
    align-items: center;

    border-radius: 15px;
    box-shadow: 0 0 5px 0 #00000050;
  }

  /* Nome do mes */
  .nomeDoMes {
    display: flex;
    flex-direction: column;

    width: 90%;
    height: 10%;
    
    background-color: rgb(187, 0, 187);

    justify-content: center;
    align-items: center;

    border-radius: 25px;

    color: #fff;
  }

  /* Semana */
  .semana {
    display: flex;
    flex-direction: row;

    width: 95%;
    height: 8%;

    justify-content: space-evenly;
    align-items: center;
  }

  /* Dia */
  .diasDoMes {
    display: flex;
    justify-content: space-evenly;
    flex-wrap: wrap;

    width: 90%;
    height: 60%;
  }
  
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

    background-color: rgb(187, 0, 187);
}

.numeroDoDia {
  display: flex;

  width: 82%;
  height: 82%;

  justify-content: center;
  align-items: center;

  border-radius: 100%;
  border: 2px solid #ffffff00;

  background-color: rgb(187, 0, 187);
  color: #fff !important;
}

.numeroDoDiaAtual {
  border: 2px solid #fff !important;
}
</style>
