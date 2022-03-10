<template>
  <div class="qs-block">
            <div class="qs-title">Top Losers</div>
            <div class="top-gainers">
              <div class="tg-item" v-for="(value) in coins.slice(0, 3)" :key="value">
                <div class="item_asset-data">
                  <img :src="value.image" loading="lazy" alt="" class="asset_icon">
                  <div class="asset_name">{{ value.name }}</div>
                  <div class="asset_ticker">{{ value.symbol }}</div>
                </div>
                <div class="item_price-data">
                  <div class="price_value">{{ currencyFormatter( value.current_price )}}</div>
                </div>
                <div class="item_listing-data">
                  <div :class="percentValueStyler(value.price_change_percentage_24h_in_currency)">{{ parseFloat( value.price_change_percentage_24h_in_currency?.toLocaleString() ).toFixed(2) }}%</div>
                </div>
              </div>
            </div>
          </div>
</template>

<script>
import axios from 'axios'

export default {

    created() {
        this.getPrice();
        this.timer = setInterval(this.getPrice, 10000);
    },

    data: () => ({
        coins: [],
        errors: [],
        timer: [],
    }),

    methods: {
        async getPrice() {
            axios
            .get('https://coindata.ddns.net/scripts/coinstats.php')
            .then(response => { 
              this.coins = response.data.sort((a, b) => parseFloat(a.price_change_percentage_24h_in_currency) - parseFloat(b.price_change_percentage_24h_in_currency)); 
              console.log(response.data)
            })
            .catch(e => { this.errors.push(e)})
        },

        percentValueStyler(value) { return {
            'positivePct': value > 0 && value <= 25, 
            'positivePctLarge': value > 25,

            'negativePct': value < 0 && value >= -25, 
            'negativePctLarge': value < -25,
          };
        },

        currencyFormatter(value) { return value?.toLocaleString('en-US', { style: 'currency', currency: 'USD' });
        },
    },

}
</script>

<style>

</style>