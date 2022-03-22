<template>
<div class="qs-block">
        <div class="qsb-header">
          <div class="qsb-header-left">

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
                <div class="price">${{ currency( value.current_price )}}</div>
              </div>
              <div id="w-node-_472e4662-8626-fde2-c00d-a7a47f6158f0-6bd61ad4" class="data-cell">
                <div :key="value.price_change_24h" :class="numberValueStyler(value.price_change_24h)">{{ currency(value.price_change_24h) }}</div>
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
        this.timer = setInterval(this.getPrice, 30000);
    },

    data: () => ({
        coins: [],
        errors: [],
        timer: [],
    }),

    methods: {
        async getPrice() {
            axios
            .get('https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false&price_change_percentage=1h%2C24h%2C7d')
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

        currency(value) {
            return new Intl.NumberFormat('en-IN', { maximumSignificantDigits: 4 }).format(value);
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

.w-layout-grid {
  display: -ms-grid;
  display: grid;
  grid-auto-columns: 1fr;
  -ms-grid-columns: 1fr 1fr;
  grid-template-columns: 1fr 1fr;
  -ms-grid-rows: auto auto;
  grid-template-rows: auto auto;
  grid-row-gap: 16px;
  grid-column-gap: 16px;
}

.tg-item {
  display: flex;
  padding-top: 1rem;
  padding-right: 1rem;
  padding-bottom: 1rem;
  padding-left: 1rem;
  justify-content: space-between;
  align-items: stretch;
  transition-property: background-color;
  transition-duration: 300ms;
  transition-timing-function: ease-in-out;
  color: #d1d4dc;
  cursor: pointer;
}

.tg-item:hover {
  background-color: hsla(0, 0.00%, 100.00%, 0.05);
}

.tg-item:nth-child(even) {
  background-color: rgba(0, 0, 0, 0.2);
}

.tg-item:nth-child(even):hover {
  background-color: hsla(0, 0.00%, 100.00%, 0.05);
}

.qs-block {
  position: relative;
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  height: 93vh;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -webkit-flex-direction: column;
  -ms-flex-direction: column;
  flex-direction: column;
}

.qsbh-icon {
  width: 24px;
  height: 24px;
}

.qsb-header-left {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
}

.top-gainers {
  overflow: scroll;
  padding-top: 50px;
  padding-bottom:
}

.qsb-fade {
  position: absolute;
  left: 0%;
  top: auto;
  right: 0%;
  bottom: 0%;
  height: 3rem;
  background-image: -webkit-gradient(linear, left bottom, left top, from(#1c1e29), to(hsla(0, 0%, 100%, 0)));
  background-image: linear-gradient(0deg, #1c1e29, hsla(0, 0%, 100%, 0));
}

.data-cell {
  -webkit-box-pack: end;
  -webkit-justify-content: flex-end;
  -ms-flex-pack: end;
  justify-content: flex-end;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
}

.value-increase {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  padding-right: 1rem;
  -webkit-box-pack: end;
  -webkit-justify-content: flex-end;
  -ms-flex-pack: end;
  justify-content: flex-end;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 4px;
  background-image: url('../assets/images/arrow-up-right.svg');
  background-position: 100% 50%;
  background-size: 12px;
  background-repeat: no-repeat;
  color: #00ad6b;
}

.qsb-header {
  position: absolute;
  left: 0%;
  top: 0%;
  right: 0%;
  bottom: auto;
  z-index: 10;
  display: flex;
  height: 50px;
  padding-right: 1rem;
  padding-left: 1rem;
  justify-content: space-between;
  align-items: center;
  border-bottom-style: solid;
  border-bottom-width: 1px;
  border-bottom-color: @swatch_2e665c84;
  background-color: hsla(224, 15.15%, 19.41%, 0.70);
  backdrop-filter: blur(5px);
  color: white;
  font-size: 13px;
  font-weight: 400;
}

.price-data-grid {
  grid-column-gap: 4px;
  grid-row-gap: 4px;
  grid-template-areas: "Area Area"
    "Area-2 Area-3";
  grid-template-columns: max-content;
}

.asset-data-grid {
  margin-right: 1rem;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  grid-column-gap: 12px;
  grid-row-gap: 4px;
  grid-template-areas: "Area Area-2"
    "Area Area-3";
  -ms-grid-columns: 40px 12px 1fr;
  grid-template-columns: 40px 1fr;
  -ms-grid-rows: max-content 4px auto;
  grid-template-rows: -webkit-max-content auto;
  grid-template-rows: max-content auto;
}

.symbol-logos {
  position: relative;
  width: 36px;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
}

.asset-logo {
  position: absolute;
  left: 2px;
  top: 2px;
  right: 0px;
  bottom: 0px;
  z-index: 1;
  display: block;
  width: 24px;
  height: 24px;
  min-height: 24px;
  min-width: 24px;
  border-top-left-radius: 100%;
  border-top-right-radius: 100%;
  border-bottom-left-radius: 100%;
  border-bottom-right-radius: 100%;
  background-color: white;
}

.usdt-logo {
  position: absolute;
  left: 12px;
  top: 12px;
  right: 0px;
  bottom: 0px;
  display: block;
  width: 24px;
  height: 24px;
  min-height: 24px;
  min-width: 24px;
  border-radius: 100%;
}

.symbol-pairs {
  text-transform: uppercase;
}

.symbol-pairs-long {
  color: rgba(209, 212, 220, 0.6);
}

#w-node-ae35288a-8d5a-db7e-7897-48bd95956176-6bd61ad4 {
  -ms-grid-row: 1;
  -ms-grid-column: 1;
  -ms-grid-column-span: 3;
  grid-area: Area;
  -ms-grid-row-align: stretch;
  align-self: stretch;
  -ms-grid-column-align: center;
  justify-self: center;
}

.asset-data-grid>#w-node-ae35288a-8d5a-db7e-7897-48bd95956176-6bd61ad4 {
  -ms-grid-row: 1;
  -ms-grid-row-span: 3;
  -ms-grid-column: 1;
  -ms-grid-column-span: 1;
}

#w-node-_25e8b672-effa-51d5-2d27-2d731e85bb8e-6bd61ad4 {
  -ms-grid-row: 3;
  -ms-grid-column: 1;
  grid-area: Area-2;
}

.asset-data-grid>#w-node-_25e8b672-effa-51d5-2d27-2d731e85bb8e-6bd61ad4 {
  -ms-grid-row: 1;
  -ms-grid-column: 3;
}

#w-node-_972c6198-051d-a38d-b594-bc41ec28b5b5-6bd61ad4 {
  -ms-grid-row: 3;
  -ms-grid-column: 3;
  grid-area: Area-3;
}

.asset-data-grid>#w-node-_972c6198-051d-a38d-b594-bc41ec28b5b5-6bd61ad4 {
  -ms-grid-row: 3;
  -ms-grid-column: 3;
}

#w-node-fdc8b29f-7693-d8e9-ba29-ada352c6f265-6bd61ad4 {
  -ms-grid-row: 1;
  -ms-grid-column: 1;
  -ms-grid-column-span: 3;
  -ms-grid-column-align: end;
  justify-self: end;
  grid-area: Area;
}

.asset-data-grid>#w-node-fdc8b29f-7693-d8e9-ba29-ada352c6f265-6bd61ad4 {
  -ms-grid-row: 1;
  -ms-grid-row-span: 3;
  -ms-grid-column: 1;
  -ms-grid-column-span: 1;
}

#w-node-_472e4662-8626-fde2-c00d-a7a47f6158f0-6bd61ad4 {
  -ms-grid-column-align: end;
  justify-self: end;
  -ms-grid-column: span 1;
  grid-column-start: span 1;
  -ms-grid-column-span: 1;
  grid-column-end: span 1;
  -ms-grid-row: span 1;
  grid-row-start: span 1;
  -ms-grid-row-span: 1;
  grid-row-end: span 1;
}

#w-node-_2c4cd426-a529-68bf-34ab-7a7f57ee277d-6bd61ad4 {
  -ms-grid-column-align: end;
  justify-self: end;
  -ms-grid-column: span 1;
  grid-column-start: span 1;
  -ms-grid-column-span: 1;
  grid-column-end: span 1;
  -ms-grid-row: span 1;
  grid-row-start: span 1;
  -ms-grid-row-span: 1;
  grid-row-end: span 1;
}
</style>