<template>
  <div class="qs-block gainers">
          <div class="qsb-header">
            <div class="qsb-header-left">
              <div data-w-id="6a4f276c-5947-d62f-32dc-ff1f339fb101" data-animation-type="lottie" data-src="../assets/documents/trending-down.json" data-loop="0" data-direction="1" data-autoplay="1" data-is-ix2-target="0" data-renderer="svg" data-default-duration="1.0166666666666666" data-duration="0" class="lottie-animation"></div>
              <div>Greatest Gainers</div>
            </div><img src="images/last-24-hours-96.png" loading="lazy" alt="" class="qsbh-icon">
          </div>
          <div class="top-gainers">
            <div class="tg-item" v-for="(value) in coins.slice(0,20)" :key="value">
              <div class="item_asset-data">
                  <img :src="value.image" loading="lazy" alt="" class="asset_icon">
                <div class="asset_name">{{ value.name }}</div>
                <div class="asset_ticker">{{ value.symbol }}</div>
              </div>
              <div class="item_price-data">
                <div class="dynamic-value-small" :key="value.current_price">{{ currencyFormatter( value.current_price )}}</div>
              </div>
              <div class="item_listing-data">
                <div :class="percentValueStyler(value.price_change_percentage_24h_in_currency)">{{ parseFloat( value.price_change_percentage_24h_in_currency?.toLocaleString() ).toFixed(2) }}%</div>
              </div>
            </div>
          </div>
          <div class="qsb-fade"></div>
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
              this.coins = response.data.sort((b, a) => parseFloat(a.price_change_percentage_24h_in_currency) - parseFloat(b.price_change_percentage_24h_in_currency)); 
              console.log(response.data)
            })
            .catch(e => { this.errors.push(e)})
        },

        percentValueStyler(value) { return {
            'positivePct': value > 0,
            'negativePct': value < 0
          };
        },

        currencyFormatter(value) { return value?.toLocaleString('en-US', { style: 'currency', currency: 'USD' });
        },
    },

}
</script>

<style scoped>
.dynamic-value-small {
  background-color: transparent;
  color: white;
  line-height: 18px;
  font-weight: inherit;
  animation: bgchange 3s;
}
@keyframes bgchange {
  from {
    background-color: green;
    color: white;
  } to {
    background-color: transparent;
    color: white;
  }
}
</style>