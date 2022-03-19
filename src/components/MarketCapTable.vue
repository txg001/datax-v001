<template>
  <div class="table">
          <div class="table-toolbar">
            <div class="pt-right">
              <div class="category-selectors">
                <div class="category-text">Category:</div>
                <div class="selector-button active">
                  <div>All</div>
                </div>
                <div class="selector-button">
                  <div>DeFi</div>
                </div>
                <div class="selector-button">
                  <div>Metaverse</div>
                </div>
                <div class="selector-button">
                  <div>Stablecoins</div>
                </div>
              </div>
            </div>
            <div class="search-wrapper">
              <div class="search-block w-form">

                 <input v-model="search" type="email" class="search-input w-input" placeholder="Search" id="Search-2" required="">
                  <div class="div-block-2">/</div>
  
              </div>
            </div>
          </div>
          <div class="table-head">
            <div class="cell rank"><div class="table-heading-text">#</div></div>
            <div class="asset-cell xl"><div class="table-heading-text">Name</div></div>
            <div class="cell lplus"><div class="table-heading-text">price / 24h change</div></div>
            <div class="cell l"><div class="table-heading-text">7d</div></div>
            <div class="cell l"><div class="table-heading-text">1m</div></div>
            <div class="cell l"><div class="table-heading-text">1m Volatility</div></div>
            <div class="cell xl"><div class="table-heading-text">circulating supply</div></div>
          </div>
          <div class="table-body-copy">
            <div class="table-row" v-for="value in filteredData" :key="value">
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
                  <div class="dynamic-value" :key="value.current_price">{{ currencyFormatter( value.current_price ) }}</div>
                </div>
                <div class="div-block-3">
                  <div :class="numberValueStyler(value.price_change_24h)">{{ currencyFormatter(value.price_change_24h) }}</div>
                  <div :class="numberValueStyler(value.price_change_percentage_24h_in_currency)">{{ parseFloat(value.price_change_percentage_24h_in_currency).toFixed(2) }}%</div>
                </div>
              </div>
              <div class="cell l">
                <div :class="percentValueStylerLarge(value.price_change_percentage_7d_in_currency)">{{ parseFloat( value.price_change_percentage_7d_in_currency?.toLocaleString() ).toFixed(2) }}%</div>
              </div>
              <div class="cell l">
                <div :class="percentValueStylerLarge(value.price_change_percentage_30d_in_currency)">{{ parseFloat( value.price_change_percentage_30d_in_currency?.toLocaleString() ).toFixed(2) }}%</div>
              </div>
              <div class="cell l">
                    <div class="volatility-wrap">
                      <div class="volatility-value">{{ Math.floor((value.datax.m1_vol) * 100) }}%</div>
                      <div class="volatility-bar-wrapper" :style="{height: 4 +'px'}">
                        <div :class="volatilityValueStyler( Math.floor(( value.datax.m1_vol ) * 100) )" :style="{width: Math.floor(( value.datax.m1_vol ) * 100)+'%'}"></div>
                      </div>
                    </div>
                  </div>
              <div class="cell xl">
                  <div class="value small">{{ numAbbr(value.circulating_supply) }} {{ value.symbol.toUpperCase() }}</div>
                  <div class="supply-bar-wrapper" :style="{height: 4 +'px'}">
                    <div class="supply" :style="{width: Math.floor((value.circulating_supply / value.total_supply) * 100)+'%'}"></div>
                  </div>
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
            .get('https://coindata.ddns.net/scripts/coinstats.php')
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
            'positiveNum': value > 0,
            'negativeNum': value < 0,
            'neutralNum': value = 0,
          };
        },

        numAbbr(value) {
            if (value >= 1000000000) { return (value / 1000000000).toFixed(2).replace(/\.0$/, '') + 'B'; }
            if (value >= 1000000) { return (value / 1000000).toFixed(2).replace(/\.0$/, '') + 'M'; }
            if (value >= 1000) { return (value / 1000).toFixed(2).replace(/\.0$/, '') + 'K'; }
            return value;
        },

        currencyFormatter(value) { return value?.toLocaleString('en-US', { style: 'currency', currency: 'USD' });
        },
    },

}
</script>

<style>
.dynamic-value {
  background-color: transparent;
  color: white;
  font-size: 12px;
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
</style>