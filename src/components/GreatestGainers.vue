<template>
<div class="qs-block">
        <div class="qsb-header">
          <div class="qsb-header-left">
            <div class="icon green w-embed"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewbox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-trending-up"><polyline points="23 6 13.5 15.5 8.5 10.5 1 18"></polyline><polyline points="17 6 23 6 23 12"></polyline></svg></div>
            <div>Top Movers</div>
          </div>
          <img src="../assets/images/last-24-hours-96_1last-24-hours-96.png" loading="lazy" alt="" class="qsbh-icon">
        </div>
        <div class="top-gainers">
          <div class="tg-item" v-for="(value) in coins" :key="value">
            <div class="w-layout-grid asset-data-grid">
              <div id="w-node-ae35288a-8d5a-db7e-7897-48bd95956176-6bd61ad4" class="symbol-logos">
                <img :src="value.image" loading="lazy" alt="" class="asset-logo">
                <img src="../assets/images/usdt.svg" loading="lazy" alt="" class="usdt-logo"></div>
              <div id="w-node-_25e8b672-effa-51d5-2d27-2d731e85bb8e-6bd61ad4" class="symbol-pairs">{{ value.symbol }}-USD</div>
              <div id="w-node-_972c6198-051d-a38d-b594-bc41ec28b5b5-6bd61ad4" class="symbol-pairs-long">{{ value.name }} / TetherUS</div>
            </div>
            <div class="w-layout-grid price-data-grid">
              <div id="w-node-fdc8b29f-7693-d8e9-ba29-ada352c6f265-6bd61ad4" class="data-cell">
                <div class="price">{{ currencyFormatter( value.current_price )}}</div>
              </div>
              <div id="w-node-_472e4662-8626-fde2-c00d-a7a47f6158f0-6bd61ad4" class="data-cell">
                <div :key="parseFloat(value.price_change_24h).toFixed(4)" :class="numberValueStyler(value.price_change_24h)">{{ parseFloat(value.price_change_24h).toFixed(4) }}</div>
              </div>
              <div id="w-node-_2c4cd426-a529-68bf-34ab-7a7f57ee277d-6bd61ad4" class="data-cell">
                <div :key="value.price_change_percentage_24h_in_currency" :class="numberValueStyler(value.price_change_percentage_24h_in_currency)">{{ parseFloat( value.price_change_percentage_24h_in_currency?.toLocaleString() ).toFixed(2) }}%</div>
              </div>
            </div>
          </div>
        </div>
        <div class="qsb-fade"></div>
      </div>
</template>

<script>
import axios from 'axios'

export default {

    components: {
    },

    created() {
        this.getPrice();
        this.timer = setInterval(this.getPrice, 5000);
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

        numberValueStyler(value) { return {
            'price-positive': value > 0,
            'price-negative': value < 0,
            'price-neutral': value = 0,
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

.symbol-pairs-long {
  width: 120px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.price-positive {
  color: #00ad6b;
  background-color: transparent;
  animation: pos-bgchange 2s ease-out;
}
@keyframes pos-bgchange {
  from {
    background-color: #00ad6b;
    color: white;
  } to {
    background-color: transparent;
    color: #00ad6b;
  }
}

.price-negative {
  color: #d9475a;
  background-color: transparent;
  animation: neg-bgchange 2s ease-out;
}
@keyframes neg-bgchange {
  from {
    background-color: #d9475a;
    color: white;
  } to {
    background-color: transparent;
    color: white;
  }
}

</style>