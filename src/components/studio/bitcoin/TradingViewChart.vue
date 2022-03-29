<template>
    <div id="w-node-_4b6f2c0c-8594-3d1f-d7c5-6e4e0d21c218-cd1d760e" class="studio-div-wrapper-copy">
        <Chart 
        :options="{
            width: 750,
            height: 450,
            symbol: 'BINANCE:BTCUSDT',
            theme: 'dark',
            interval: '60',
            style: 1,
            locale: 'en',
            enable_publishing: false,
            save_image: false,
        }" />      
    </div>
</template>


<script>
import { Chart } from 'vue-tradingview-widgets';

export default ({
  name: 'App',
  components: {
    Chart
  },
});
</script>

<style>

</style>