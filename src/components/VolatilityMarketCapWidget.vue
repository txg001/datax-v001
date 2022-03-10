<template>
  <div class="volatility-table_component">
      <div class="layout-1368">
        <div class="table">
          <div class="table-toolbar">
            <div class="pt-wrapper">
              <div class="pt-left">
                <div class="text-block-3">Top 100 Cryptocurrencies Sorted by 24 hour Volatility</div>
              </div>
              <div class="pt-right">
                <div class="category-selectors">
                  <div class="category-text">Category:</div>
                  <div class="selector-button active"><div>All</div></div>
                  <div class="selector-button"><div>DeFi</div></div>
                  <div class="selector-button"><div>Metaverse</div></div>
                  <div class="selector-button"><div>Stablecoins</div></div>
                </div>
                <div class="divider darker"></div>
                <div class="toolbar-button active"><div>More Filters</div>
                </div>
                <div class="search-wrapper">
                  <div class="search-block w-form">
                    <form id="email-form" name="email-form" data-name="Email Form" method="get" class="search-wrapper"><input type="email" class="search-input w-input" maxlength="256" name="Search-2" data-name="Search 2" placeholder="Search" id="Search-2" required="">
                      <div class="div-block-2">/</div>
                    </form>
                  </div>
                </div>
              </div>
            </div>
            <div class="table-head">
              <div class="cell rank"><div class="table-heading-text">#</div></div>
              <div class="asset-cell xl"><div class="table-heading-text">Name</div></div>
              <div class="cell l"><div class="table-heading-text">price</div></div>
              <div class="cell l"><div class="table-heading-text">24h % Chg</div></div>
              <div class="cell l"><div class="table-heading-text">7d % Chg</div></div>
              <div class="cell l"><div class="table-heading-text">1m % Chg</div></div>
              <div class="cell l"><div class="table-heading-text">24h Vol</div></div>
              <div class="cell l"><div class="table-heading-text">7d Vol</div></div>
              <div class="cell l"><div class="table-heading-text">1m Vol</div></div>
              <div class="cell xl"><div class="table-heading-text">circulating supply</div></div>
            </div>
          </div>
          <div class="smart-table">
            <div class="table-body">
              <div class="table-row" v-for="value in coins" :key="value.id">
                <div class="cell rank">
                  <div class="value rank">{{ value.market_cap_rank }}</div>
                </div>
                <div class="asset-cell xl">
                  <img :src="value.image" loading="lazy" alt="" class="asset-logo">
                  <div class="value assets-name">{{ value.name }}</div>
                  <div class="asset-ticker">{{ value.symbol }}</div>
                </div>
                <div class="cell l">
                  <div class="value">{{ currencyFormatter( value.current_price ) }}</div>
                  <div :class="numberValueStyler(value.price_change_24h)">{{ currencyFormatter(value.price_change_24h) }}</div>
                </div>
                <div class="cell l">
                  <div class="change-wrap">
                    <div :class="percentValueStyler(value.price_change_percentage_24h_in_currency)">{{ parseFloat( value.price_change_percentage_24h_in_currency?.toLocaleString() ).toFixed(2) }}%</div>
                  </div>
                </div>
                <div class="cell l">
                  <div class="change-wrap">
                    <div :class="percentValueStyler(value.price_change_percentage_7d_in_currency)">{{ parseFloat( value.price_change_percentage_7d_in_currency?.toLocaleString() ).toFixed(2) }}%</div>
                  </div>
                </div>
                <div class="cell l">
                  <div class="change-wrap">
                    <div :class="percentValueStyler(value.price_change_percentage_30d_in_currency)">{{ parseFloat( value.price_change_percentage_30d_in_currency?.toLocaleString() ).toFixed(2) }}%</div>
                  </div>
                </div>
                 <div class="cell l">
                    <div class="volatility-wrap">
                      <div class="volatility-value">{{ Math.floor((value.datax.h24_vol) * 100) }}%</div>
                      <div class="volatility-bar-wrapper" :style="{height: 4 +'px'}">
                        <div :class="volatilityValueStyler( Math.floor(( value.datax.h24_vol ) * 100) )" :style="{width: Math.floor(( value.datax.h24_vol ) * 100)+'%'}"></div>
                      </div>
                    </div>
                  </div>
                <div class="cell l">
                    <div class="volatility-wrap">
                      <div class="volatility-value">{{ Math.floor((value.datax.d7_vol) * 100) }}%</div>
                      <div class="volatility-bar-wrapper" :style="{height: 4 +'px'}">
                        <div :class="volatilityValueStyler( Math.floor(( value.datax.d7_vol ) * 100) )" :style="{width: Math.floor(( value.datax.d7_vol ) * 100)+'%'}"></div>
                      </div>
                    </div>
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
        </div>
      </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
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
              this.coins = response.data.sort((b, a) => parseFloat(a.datax.h24_vol) - parseFloat(b.datax.h24_vol)); 
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
  height: 27px;
  padding-right: 18px;
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
  background-size: 13px;
  background-repeat: no-repeat;
  color: #00ad6b;
  font-weight: 600;
}

.positivePctLarge {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  height: 27px;
  padding-right: 18px;
  -webkit-box-pack: end;
  -webkit-justify-content: flex-end;
  -ms-flex-pack: end;
  justify-content: flex-end;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 4px;
  background-image: url('../assets/images/on-fire.gif');
  background-position: 100% 50%;
  background-size: 13px;
  background-repeat: no-repeat;
  color: #00ad6b;
  font-weight: 800;
}

.negativePct {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  height: 27px;
  padding-right: 18px;
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
  background-size: 13px;
  background-repeat: no-repeat;
  color: #d9475a;
  font-weight: 600;
}

.negativePctLarge {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  height: 27px;
  padding-right: 18px;
  -webkit-box-pack: end;
  -webkit-justify-content: flex-end;
  -ms-flex-pack: end;
  justify-content: flex-end;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 4px;
  background-image: url('../assets/images/on-fire.gif');
  background-position: 100% 50%;
  background-size: 13px;
  background-repeat: no-repeat;
  color: #d9475a;
  font-weight: 800;
}




.negativeNum {
  color: #d9475a;
  font-size: 10px;
  font-weight: 600;
  line-height: 22.5px;
  padding-right: 16px;
  background-image: url('../assets/images/decrease-icon.svg');
  background-position: 100% 50%;
  background-size: 9px;
  background-repeat: no-repeat;
}

.positiveNum {
  color: #00ad6b;
  font-size: 10px;
  font-weight: 600;
  line-height: 22.5px;
  padding-right: 16px;
  background-image: url('../assets/images/increase-icon.svg');
  background-position: 100% 50%;
  background-size: 9px;
  background-repeat: no-repeat;
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