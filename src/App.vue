<template>
  <div id="app">
    <span>Курс валют</span>
     <template v-if="currencies">
       <hr>
    <div id="USD" >Доллар США $ — {{getDollar()}} руб.</div>
    <div id="EUR">Евро € — {{getEuro()}} руб.</div>
  </template>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  name: 'App',
  data() {
    return {
      currencies: {
        Valute: {
          USD: {
            Value: 1,
          },
          EUR: {
            Value: 2,
          },
        }
      },
    }
  },
  mounted() {
   (async () => {
    let response = await fetch('https://www.cbr-xml-daily.ru/daily_json.js')
    this.currencies = await response.json(); //?
    })()
  },
  methods: {
     getDollar() {
      return this.currencies.Valute.USD.Value.toFixed(4).replace('.', ',');
    },
    getEuro() {
      return this.currencies.Valute.EUR.Value.toFixed(4).replace('.', ',');
    },
  }
})

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
