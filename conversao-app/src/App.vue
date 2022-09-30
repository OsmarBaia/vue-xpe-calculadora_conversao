<!--HTML-->
<template>
  <h1 class="label-title">Conversor de Moedas</h1>
  <h2 class="label-subtitle">Digite a quantidade a ser convertida: </h2>
  <div class="userInput">
    <span class="p-float-label">
      <InputText id="input-amount" type="text" v-model="amount" :disabled="convertedAmount"/>
      <label for="input-amount">Valor</label>
    </span>
  </div>
  <div class="userInput">
     <span class="p-float-label">
       <InputText id="input-rate" type="text" v-model="conversionRate" :disabled="convertedAmount"/>
       <label for="input-rate">Cotação</label>
     </span>
  </div>
  <div v-show="convertedAmount !== null" class="result-msg label-subtitle">
    <p>Com R${{amount}} é possível comprar ${{convertedAmount}} dólares, custando R${{conversionRate}} cada </p>
  </div>
   <div class="btn-calc">
    <PrimeButton v-if="convertedAmount === null" label="Converter" @click="CalculateConversion" :disabled="ValidateConversionRate"/>
    <PrimeButton v-else label="Limpar" @click="ResetValores"/>
  </div>
</template>

<!--JavaScript-->
<script>
export default {
  data() {
    return {
      amount: null,
      conversionRate: null,
      convertedAmount: null,
    }
  },

  methods: {
    CalculateConversion: function () {
      if (this.conversionRate > 0) {
        this.convertedAmount = (this.amount / this.conversionRate).toFixed(2);
      }
    },

    ResetValores: function () {
      this.amount = null;
      this.conversionRate = null;
      this.convertedAmount = null;
    }
  },


  computed: {
    ValidateConversionRate() {
      return this.conversionRate === null || this.conversionRate <= "0";
    }
  }
}

</script>

<!--CSS-->
<style>
*{
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.userInput{
  margin: 2rem 0.1rem;
}

PrimeButton{
  margin: 0 0.1rem;
}

.label-title{
  font-size: 2rem;
}

.label-subtitle{
  font-size: 1.2rem;
}
</style>
