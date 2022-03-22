<template>
<div class="table">
    <div class="table-toolbar">
      <div class="pt-right">
        <div class="category-selectors">
          <div class="category-text">Category:</div>
          <a href="index.html" aria-current="page" class="button margin-right w-button w--current">All Coins</a>
          <a href="#" class="button margin-right w-button">DeFi</a>
          <a href="#" class="button margin-right w-button">Metaverse</a>
          <a href="#" class="button margin-right w-button">Stablecoins</a>
        </div>
      </div>
      <div class="search-wrapper">
        <div class="search-block w-form">

            <input v-model="search" class="search-input w-input" placeholder="Search" id="Search">
            <div class="div-block-2">/</div>

        </div>
      </div>
    </div>
    <div class="table-head">
      <div class="cell rank">
        <div class="table-heading-text">#</div>
      </div>
      <div class="asset-cell xl">
        <div class="table-heading-text">Name</div>
      </div>
      <div class="cell lplus">
        <div class="table-heading-text">price / 1h change</div>
      </div>
      <div class="cell m first">
        <div class="table-heading-text">24h %</div>
      </div>
      <div class="cell m">
        <div class="table-heading-text">7D %</div>
      </div>
      <div class="cell m">
        <div class="table-heading-text">1Y %</div>
      </div>
      <div class="cell m first">
        <div class="table-heading-text">24h Vol</div>
      </div>
      <div class="cell m">
        <div class="table-heading-text">Mkt Cap</div>
      </div>
      <div class="cell l">
        <div class="table-heading-text">circulating supply</div>
      </div>
      <div class="cell l">
        <div class="table-heading-text">7D Chart</div>
      </div>
    </div>
    <div class="table-body">
      <div class="table-row" v-for="(value) in filteredData" :key="value">
        <div class="cell rank">
          <div class="value rank">{{ value.market_cap_rank }}</div>
        </div>
        <div class="asset-cell xl">
          <img :src="value.image" loading="lazy" alt="" class="asset-logo">
          <div class="value assets-name">{{ value.name }}</div>
          <div class="asset-ticker">{{ value.symbol }}</div>
        </div>
        <div class="cell lplus">
          <div class="price-box">
            <div class="value">${{ currency( value.current_price ) }}</div>
          </div>
          <div class="div-block-3">
            <div :class="numberValueStyler(value.price_change_24h)">{{ currency(value.price_change_24h) }}</div>
            <div :class="numberValueStyler(value.price_change_percentage_1h_in_currency)">{{ parseFloat(value.price_change_percentage_1h_in_currency).toFixed(4) }}%</div>
          </div>
        </div>
        <div class="cell m first">
          <div :class="numberValueStyler(value.price_change_percentage_24h_in_currency)">{{ parseFloat(value.price_change_percentage_24h_in_currency).toFixed(2) }}%</div>
        </div>
        <div class="cell m">
          <div :class="numberValueStyler(value.price_change_percentage_7d_in_currency)">{{ parseFloat(value.price_change_percentage_7d_in_currency).toFixed(2) }}%</div>
        </div>
        <div class="cell m">
          <div :class="numberValueStyler(value.price_change_percentage_1y_in_currency)">{{ parseFloat(value.price_change_percentage_1y_in_currency).toFixed(2) }}%</div>
        </div>
        <div class="cell m first">
          <div class="value small">${{ numAbbr(value.total_volume) }}</div>
        </div>
        <div class="cell m">
          <div class="value small">${{ numAbbr(value.market_cap) }}</div>
        </div>
        <div class="cell l">
              <div class="value small">{{ numAbbr(value.circulating_supply) }} {{ value.symbol.toUpperCase() }}</div>
              <div class="supply-bar-wrapper" :style="{height: 4 +'px'}">
                <div class="supply" :style="{width: Math.floor((value.circulating_supply / value.total_supply) * 100)+'%'}"></div>
              </div>
            </div>
        <div class="cell l">
          <sparkline v-bind:data="[2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31]"></sparkline>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Sparkline from './Sparkline.vue'
import axios from 'axios'


export default {

    components: {
      Sparkline
    },

    created() {
        this.getPrice();
        this.timer = setInterval(this.getPrice, 15000);
    },

    data: () => ({
        search: '',
        coins: [],
        errors: [],
        timer: [],
    }),

    computed: {
      filteredData() {
        return this.coins
          .filter(
            ({ name, symbol }) => [name, symbol]
              .some(val => val.toLowerCase().includes(this.search))
          );
        }
    },

    methods: {
        async getPrice() {
            axios
            .get('https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=true&price_change_percentage=1h%2C24h%2C7d%2C14d%2C30d%2C200d%2C1y')
            .then(response => { 
              this.coins = response.data;
              console.log(response.data)
            })
            .catch(e => { this.errors.push(e)})
        },

        percentValueStyler(value) { return {
            'positivePct': value > 0,
            'negativePct': value < 0
          };
        },

        percentValueStylerLarge(value) { return {
            'positivePctLarge': value > 0,
            'negativePctLarge': value < 0
          };
        },

        volatilityValueStyler(value) { return {
            'lowVol': value > 0 && value <= 25, 
            'mediumVol': value > 25 && value <= 50,
            'highVol': value > 50 && value <= 75,
            'extremeVol': value > 75 && value <= 100,
          };
        },

        numberValueStyler(value) { return {
            'price-positive': value > 0,
            'price-negative': value < 0,
            'price-neutral': value = 0,
          };
        },

        currency(value) {
            return new Intl.NumberFormat('en-IN', { maximumSignificantDigits: 6 }).format(value);
        },

        numAbbr(value) {
            if (value >= 1000000000) { return (value / 1000000000).toFixed(2).replace(/\.0$/, '') + 'B'; }
            if (value >= 1000000) { return (value / 1000000).toFixed(2).replace(/\.0$/, '') + 'M'; }
            if (value >= 1000) { return (value / 1000).toFixed(2).replace(/\.0$/, '') + 'K'; }
            return value;
        },

        currencyFormatter(value) { 
            return value?.toLocaleString('en-US', { style: 'currency', currency: 'USD' });
        },
    },

}
</script>

<style scoped>
.price-positive {
  padding-left: 8px;
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
  padding-left: 8px;
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

.lowVol {
  width: 90.36%;
  height: 100%;
  border-radius: 25px;
  background-color: #ced6e4;
  background-image: linear-gradient(225deg,#00aeff,rgba(0, 174, 255, 0.5) 75%);
}
.mediumVol {
  width: 90.36%;
  height: 100%;
  border-radius: 25px;
  background-color: #ced6e4;
  background-image: linear-gradient(225deg,#00ff88,rgba(0, 255, 136, 0.5) 75%);
}
.highVol {
  width: 90.36%;
  height: 100%;
  border-radius: 25px;
  background-color: #ced6e4;
  background-image: linear-gradient(225deg,#ffd900,rgba(255, 217, 0, 0.5) 75%);
}
.extremeVol {
  width: 90.36%;
  height: 100%;
  border-radius: 25px;
  background-color: #ced6e4;
  background-image: linear-gradient(225deg,#ff0000,rgba(255, 0, 0, 0.5) 75%);
}

.percentage-cell {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  width: 80px;
  padding: 6px 8px;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 8px;
  background-color: #e9ebf1;
  line-height: 21px;
}

.positivePct {
    display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  padding-right: 18px;
  padding-left: 18px;
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
  background-size: 11px;
  background-repeat: no-repeat;
  color: #00ad6b;
}

.negativePct {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  padding-right: 18px;
  padding-left: 18px;
  -webkit-box-pack: end;
  -webkit-justify-content: flex-end;
  -ms-flex-pack: end;
  justify-content: flex-end;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 4px;
  background-image: url('../assets/images/arrow-down-right.svg');
  background-position: 100% 50%;
  background-size: 11px;
  background-repeat: no-repeat;
  color: #d9475a;
}

.positivePctLarge {
  display: flex;
  padding-right: 18px;
  justify-content: flex-end;
  align-items: center;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
  background-image: url('../assets/images/arrow-up-right.svg');
  background-position: 100% 50%;
  background-size: 13px;
  background-repeat: no-repeat;
  color: hsla(157, 100.00%, 34.00%, 1.00);
}

.negativePctLarge {
  display: flex;
  padding-right: 18px;
  justify-content: flex-end;
  align-items: center;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
  background-image: url('../assets/images/arrow-down-right.svg');
  background-position: 100% 50%;
  background-size: 13px;
  background-repeat: no-repeat;
  color: #d9475a;
}

.negativeNum {
  padding-right: 14px;
  padding-left: 8px;
  font-size: 10px;
  line-height: 18px;
  background-image: url('../assets/images/decrease-icon.svg');
  background-position: 100% 50%;
  background-size: 10px;
  background-repeat: no-repeat;
  color: #d9475a;
}

.positiveNum {
  padding-right: 14px;
  padding-left: 8px;
  font-size: 10px;
  line-height: 18px;

  background-image: url('../assets/images/increase-icon.svg');
  background-position: 100% 50%;
  background-size: 10px;
  background-repeat: no-repeat;
  color: #00ad6b;
}

.neutralNum {
  color: #7b849b;
  font-size: 12px;
  line-height: 22.5px;
}

.neutralPct {
  background-color: rgba(255, 255, 255, 0);
  color: #7b849b;
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  width: 80px;
  padding: 6px 8px;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 8px;
  line-height: 21px;
}






.table-head {
  position: -webkit-sticky;
  position: sticky;
  top: 7vh;
  z-index: 10;
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  height: 50px;
  padding: 1rem;
  -webkit-box-align: stretch;
  -webkit-align-items: stretch;
  -ms-flex-align: stretch;
  align-items: stretch;
  border-bottom: 1px solid #434651;
  background-color: rgba(42, 46, 57, 0.25);
  box-shadow: none;
  -webkit-backdrop-filter: blur(5px);
  backdrop-filter: blur(5px);
  color: #d1d4dc;
  font-size: 10px;
  font-weight: 400;
  text-transform: capitalize;
}

.div-block-2 {
  position: absolute;
  left: auto;
  top: 0%;
  right: 0%;
  bottom: 0%;
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  width: 21px;
  height: 21px;
  margin-top: auto;
  margin-right: 10px;
  margin-bottom: auto;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 4px;
  background-color: rgba(201, 207, 221, 0.15);
  color: #fff;
  font-size: 11px;
  font-weight: 600;
}

.search-wrapper {
  position: relative;
}

.asset-logo {
  display: block !important;
  width: 21px;
  height: 21px;
  margin-right: 10px;
  border-top-left-radius: 100%;
  border-top-right-radius: 100%;
  border-bottom-left-radius: 100%;
  border-bottom-right-radius: 100%;
}

.table-toolbar {
  position: -webkit-sticky;
  position: sticky;
  top: 0px;
  z-index: 10;
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  height: 7vh;
  padding-right: 1rem;
  padding-left: 1rem;
  -webkit-box-pack: justify;
  -webkit-justify-content: space-between;
  -ms-flex-pack: justify;
  justify-content: space-between;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-bottom: 1px solid #434651;
  background-color: rgba(42, 46, 57, 0.51);
  -webkit-backdrop-filter: blur(5px);
  backdrop-filter: blur(5px);
}

.category-text {
  margin-right: 0.8rem;
  color: hsla(0, 0%, 100%, 0.5);
  line-height: 14px;
}

.supply-bar-wrapper {
  width: 100px;
  height: 4px;
  margin-top: 4px;
  border-radius: 25px;
  background-color: rgba(233, 235, 241, 0.1);
}

.div-block-3 {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
}

.category-selectors {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
}

.value.rank {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  height: 24px;
  padding-right: 8px;
  padding-left: 8px;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 25%;
  background-color: rgba(16, 18, 25, 0.6);
  color: hsla(0, 0%, 100%, 0.5);
  font-size: 10px;
  line-height: 12px;
}

.value.assets-name {
  margin-right: 6px;
}

.pt-right {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: start;
  -webkit-justify-content: flex-start;
  -ms-flex-pack: start;
  justify-content: flex-start;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  -webkit-box-flex: 1;
  -webkit-flex: 1;
  -ms-flex: 1;
  flex: 1;
}

.value-positive {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  padding-left: 18px;
  -webkit-box-pack: end;
  -webkit-justify-content: flex-end;
  -ms-flex-pack: end;
  justify-content: flex-end;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 4px;
  background-image: url('../assets/images/increase-icon.svg');
  background-position: 0% 50%;
  background-size: 13px;
  background-repeat: no-repeat;
  color: #00ad6b;
}

.table-row {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  padding: 1.2rem 1rem;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  -webkit-transition: all 300ms ease-in-out;
  transition: all 300ms ease-in-out;
  color: #d1d4dc;
  font-weight: 400;
}

.table-row:hover {
  background-color: hsla(0, 0%, 100%, 0.05);
}

.table {
  position: relative;
  overflow: scroll;
  height: 100vh;
  min-height: 100vh;
  padding-bottom: 1rem;
  border-right: 1px solid #434651;
  border-bottom: 1px solid #101219;
  border-left: 1px solid #434651;
  background-color: #1c1e29;
}

.supply {
  width: 90.36%;
  height: 100%;
  border-radius: 25px;
  background-color: #1b72e3;
}

.search-input {
  width: 240px;
  margin-bottom: 0px;
  padding-left: 40px;
  border: 1px none #000;
  border-radius: 4px;
  background-color: hsla(0, 0%, 100%, 0.1);
  background-image: url('../assets/images/search.svg');
  background-position: 12px 50%;
  background-size: 18px;
  background-repeat: no-repeat;
  -webkit-transition: all 300ms ease-in-out;
  transition: all 300ms ease-in-out;
}

.search-input:hover {
  background-color: #353944;
}

.search-input::-webkit-input-placeholder {
  color: #80868f;
}

.search-input:-ms-input-placeholder {
  color: #80868f;
}

.search-input::-ms-input-placeholder {
  color: #80868f;
}

.search-input::placeholder {
  color: #80868f;
}

.price-box {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  padding: 0rem;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -webkit-flex-direction: column;
  -ms-flex-direction: column;
  flex-direction: column;
  -webkit-box-align: end;
  -webkit-align-items: flex-end;
  -ms-flex-align: end;
  align-items: flex-end;
}

.asset-ticker {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  opacity: 0.6;
  color: #80868f;
  text-transform: uppercase;
}

.search-block {
  margin-bottom: 0px;
  margin-left: 1rem;
}

.cell {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  width: 120px;
  height: 100%;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -webkit-flex-direction: column;
  -ms-flex-direction: column;
  flex-direction: column;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: end;
  -webkit-align-items: flex-end;
  -ms-flex-align: end;
  align-items: flex-end;
}

.cell.lplus {
  width: 140px;
}

.cell.m {
  width: 80px;
}

.cell.m.first {
  width: 90px;
}

.cell.xl {
  width: 150px;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -webkit-flex-direction: column;
  -ms-flex-direction: column;
  flex-direction: column;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: end;
  -webkit-align-items: flex-end;
  -ms-flex-align: end;
  align-items: flex-end;
}

.cell.rank {
  width: 40px;
  -webkit-box-align: start;
  -webkit-align-items: flex-start;
  -ms-flex-align: start;
  align-items: flex-start;
  background-color: transparent;
}

.cell.l {
  width: 140px;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -webkit-flex-direction: column;
  -ms-flex-direction: column;
  flex-direction: column;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: end;
  -webkit-align-items: flex-end;
  -ms-flex-align: end;
  align-items: flex-end;
}

.asset-cell {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  width: 120px;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
  -webkit-flex-direction: row;
  -ms-flex-direction: row;
  flex-direction: row;
  -webkit-box-pack: start;
  -webkit-justify-content: flex-start;
  -ms-flex-pack: start;
  justify-content: flex-start;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
}

.asset-cell.xl {
  width: 200px;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  -webkit-box-flex: 1;
  -webkit-flex: 1;
  -ms-flex: 1;
  flex: 1;
}

.body {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  background-color: #000;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Fira Sans', 'Droid Sans', 'Helvetica Neue', sans-serif;
  font-size: 12px;
}

.button {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  -webkit-box-flex: 1;
  -webkit-flex: 1;
  -ms-flex: 1;
  flex: 1;
  border-radius: 4px;
  background-color: rgba(255, 255, 255, 0.1);
  color: #adadad;
  text-align: center;
  white-space: nowrap;
}

.button.w--current {
  background-color: #1b72e3;
  color: #fff;
}

.button.margin-right {
  margin-right: 6px;
}

.small-value-positive {
  padding-left: 8px;
  color: #00ad6b;
  line-height: 18px;
}

@media screen and (max-width: 991px) {
  .table {
    border-top: 1px solid #373a45;
  }
}

@media screen and (max-width: 767px) {
  .cell.m {
    display: none;
  }
}

@media screen and (max-width: 479px) {
  .cell.xl {
    display: none;
  }

  .cell.l {
    display: none;
  }
}
</style>