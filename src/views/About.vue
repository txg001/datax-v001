<template>
<div>
  <div v-for="trades in trades" :key="trades">
      <div>{{ trades.price }}</div>
      <div>{{ trades.quoteQty }} BTC</div>
      <div>{{  }}</div>
  </div>
</div>
</template>

<script> 
import axios from 'axios'
export default {

    components: {
    },

    created() {
        this.getTrades();
        this.timer = setInterval(this.getTrades, 3000);
    },

    data: () => ({
        trades: [],
        errors: [],
        timer: [],
    }),

    methods: {
        async getTrades() {
            axios
            .get('https://api.binance.com/api/v3/trades?symbol=BTCUSDT')
            .then(response => { 
              this.trades = response.data; 
              console.log(response.data)
            })
            .catch(e => { this.errors.push(e)})
        },


    },

}
</script>

<style>

</style>
