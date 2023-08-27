<template>
  <div id="calendario">
    <!-- Nome do Mes -->
    <NomeDoMes :nomeDesteMes="nomeDesteMes" />
    <!-- Semanas -->
    <div class="semana">
      <div v-for="semana in semanaItens" :key="semana.id">
          <h3>{{ semana.id }}</h3>
      </div>
    </div>

    <div class="diasDoMes">
      <!-- Dias do mes anterior -->
      <div v-for="diasVaziosAnteriores in diasNoMesAnterior" :key="diasVaziosAnteriores.id">
        <div :id="diasVaziosAnteriores.id" class="diaEmBranco"></div>
      </div>
      
      <!-- Dias do mes atual -->
      <div v-for="dias in diasNoMesAtual" :key="dias.id">
        <Dia :numeroDoDia="dias.nomeDoItem" :diaID="dias.id" />
      </div>
      
      <!-- Dias do mes posterior -->
      <div v-for="diasVaziosPosteriores in diasNoMesPosterior" :key="diasVaziosPosteriores.id">
        <div :id="diasVaziosPosteriores.id" class="diaEmBranco"></div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import dayjs from 'dayjs';

import NomeDoMes from './NomeDoMes.vue';
import Dia from './Dia.vue';

export default {
  name: "Mes",
  components: {
    NomeDoMes,
    Dia
  },
  data() {
    return {
      /* Mes */
      meses: new Array("Janeiro","Fevereiro","Marco","Abril","Maio","Junho","Julho","Agosto","Septembro","Outubro","Novembro","Dezembro"),
      nomeDesteMes: "",
      diasNoMesAnterior: [{id: ""}],
      diasNoMesAtual: [{id: "", nomeDoItem: ""}],
      diasNoMesPosterior: [{id: ""}],

      /* Semana */
      semanaItens: new Array({id: "Dom"}, {id: "Seg"}, {id: "Ter"}, {id: "Qua"}, {id: "Qui"}, {id: "Sex"}, {id: "Sáb"}),
    }
  },
  methods: {
    /* Setar nome do mes */
    async nomeDoMes() {
      const mesAtual = dayjs().startOf("month").toDate()
      const checarMesAtual = parseInt(dayjs(mesAtual).format("MM"))
      this.nomeDesteMes = this.meses[(checarMesAtual - 1)].toUpperCase()
    },

    /* Setar mes atual */
    async mesAtual() {
      const dataAtual = dayjs().startOf("day").toDate()
      const checarMesAtual = dayjs(dataAtual).format("YYYY-MM-DD")
      let diasNoMes = dayjs(`${checarMesAtual}`).daysInMonth()
      this.diasNoMesAtual.shift()
      for(let i = 1; i < (diasNoMes + 1); i++) {
        this.diasNoMesAtual.push({id: `${i}`, nomeDoItem: `itemN${i}`})
      }
      /* Renderizar itens */
      document.addEventListener("DOMContentLoaded", function () {
        document.getElementById(`itemN${parseInt(dayjs(dataAtual).format("DD"))}`)?.classList.add("numeroDoDiaAtual")
      })
    },

    /* Setar mes anterior */
    async mesAnterior() {
      const dataAtual = dayjs().startOf("day").toDate()
      const mesAtual = dayjs().startOf("month").toDate()
      const formatarMes = dayjs(mesAtual).format("MM")
      let mesAnterior
      if(parseInt(formatarMes) == 1) {
        mesAnterior = dayjs(dataAtual).format(`YYYY-${12}-${2}`)
      } else {
        mesAnterior = dayjs(dataAtual).format(`YYYY-${parseInt(formatarMes) - 1}-${2}`)
      }
      const pegarDiasAnteriores = dayjs(mesAnterior).daysInMonth()
      const calcMesAnterior = this.diasNoMesAtual.length - pegarDiasAnteriores

      this.diasNoMesAnterior.shift()
      for(let i = 1; i < (calcMesAnterior + 1); i++) {
        this.diasNoMesAnterior.push({id: `${i}`})
      }
    },

    /* Setar mes posterior */
    async mesPosterior() {
      const dataAtual = dayjs().startOf("day").toDate()
      const mesAtual = dayjs().startOf("month").toDate()
      const formatarMes = dayjs(mesAtual).format("MM")
      let mesPosterior
      if(parseInt(formatarMes) == 1) {
        mesPosterior = dayjs(dataAtual).format(`YYYY-${12}-${2}`)
      } else {
        mesPosterior = dayjs(dataAtual).format(`YYYY-${parseInt(formatarMes) - 1}-${2}`)
      }
      const pegarDiasPosteriores = dayjs(mesPosterior).daysInMonth()
      const calcMesPosterior = this.diasNoMesAtual.length - pegarDiasPosteriores

      this.diasNoMesPosterior.shift()
      for(let i = 1; i < (calcMesPosterior + 1); i++) {
        this.diasNoMesPosterior.push({id: `${i}`})
      }
    },
  },
  mounted() {
    this.nomeDoMes()
    this.mesAtual()
    this.mesAnterior()
    this.mesPosterior()
     
  }
}
</script>

<style scoped>
/* Calendario */
#calendario {
  display: flex;
  flex-direction: column;

  width: 33vw;
  height: 75vh;
  min-height: 500px;
  height: 70%;

  justify-content: space-evenly;
  align-items: center;

  border-radius: 15px;
  box-shadow: 0 0 5px 0 #00000050;
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

  /* Dias no mes */
.diasDoMes {
  display: flex;
  justify-content: space-evenly;
  flex-wrap: wrap;

  width: 90%;
  height: 60%;
}

/* Dias vazios */
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
