<template>
<div class="qs-block">
        <div class="qsb-header">
          <div class="qsb-header-left">
            <div>Large BTC Trades</div>
          </div>
            <select @change="e => $emit('input', e.target.tradeFilter)" v-model="tradeFilter" id="field" name="field" data-name="Field" class="select-field">
              <option :value="0">No Filter</option>
              <option :value="1000">> 1000</option>
              <option :value="10000">> 10,000</option>
              <option :value="100000">> 100,000</option>
            </select>
        </div>
        <div class="top-gainers">
          <div v-for="trades in filteredTrades" :key="trades">

            <div class="tg-item" :class="tradeDivStyler(trades.isBuyerMaker)">
              <div id="large-trade-grid" class="w-layout-grid large-trade-grid">
                <div id="w-node-b736b7d6-0c81-c102-1fde-dd42ddff419b-53bf46aa" class="data-cell">
                  <div class="text">Bitcoin / TetherUS</div>
                  <div class="muted-text">Binance.com</div>
                  <div class="muted-text small">{{ trades.time }}</div>
                </div>
                <div id="w-node-_2c7ab8d7-3d94-eb89-3828-6f933102b1d1-53bf46aa" class="data-cell-right">
                  <div class="text">${{ currency(trades.quoteQty) }}</div>
                  <div class="muted-text">{{ trades.qty }} BTC</div>
                </div>
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
        this.getTrades();
        this.timer = setInterval(this.getTrades, 3000);
    },

    data: () => ({
        trades: [],
        errors: [],
        timer: [],
        isMarketMaker: true,
        tradeFilter: 0,
    }),

    computed: {
      filteredTrades() {
              return this.trades.filter(trades => trades.quoteQty > this.tradeFilter);
      }
    },

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

        tradeDivStyler(value) { 
            return {
            'market-maker': value === true,
            'market-taker': value === false
          };
        },

        largeTradeFilter(value) { 
            return {
            't10000': value > 10000,
            'market-taker': value === false
          };
        },

        currency(value) {
            return new Intl.NumberFormat('en-IN', { maximumSignificantDigits: 4 }).format(value);
        },

    },

}
</script>


<style scoped>

.data-cell-right {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-end;
}

.Block:local-styles {
  justify-self: end;
  grid-area: Area-2;
}
.text {
  color: #d1d4dc;
}

.muted-text {
  color: hsla(223.63636363636357, 13.58%, 84.12%, 0.60);
}

.muted-text.small {
  color: hsla(223.63636363636357, 13.58%, 84.12%, 0.50);
  font-size: 10px;
  line-height: 21px;
}

select {
    appearance: none !important;
    -webkit-appearance: none !important;
    -moz-appearance: none !important;
  }

.select-field {
  padding: 9px 1.5rem 9px 1rem;
  border: 1px none #000;
  border-radius: 4px;
  background-color: hsla(0, 0%, 100%, 0);
  background-image: url('../assets/images/chevron-down-3.svg');
  background-position: 95% 50%;
  background-size: 12px;
  background-repeat: no-repeat;
  color: #fff;
  font-size: 12px;
}
.market-maker {
    background-color: hsla(157, 100%, 34%, 0.1);
}
.market-taker {
    background-color: hsla(352, 66%, 56%, 0.1);
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
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  padding: 1rem;
  -webkit-box-pack: justify;
  -webkit-justify-content: space-between;
  -ms-flex-pack: justify;
  justify-content: space-between;
  -webkit-box-align: stretch;
  -webkit-align-items: stretch;
  -ms-flex-align: stretch;
  align-items: stretch;
  border-bottom: 1px solid #1c1e29;
  -webkit-transition: background-color 300ms ease-in-out;
  transition: background-color 300ms ease-in-out;
  color: #d1d4dc;
  cursor: pointer;
}

.tg-item:hover {
  background-color: hsla(0, 0%, 100%, 0.05);
}

.tg-item.buy {
  background-color: rgba(0, 173, 107, 0.1);
}

.tg-item.sell {
  background-color: rgba(217, 71, 90, 0.1);
}

.hotbar {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  min-width: 350px;
  padding: 0rem;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -webkit-flex-direction: column;
  -ms-flex-direction: column;
  flex-direction: column;
  border-right: 1px solid #434651;
  background-color: #1c1e29;
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
  padding-bottom: 3rem;
  -webkit-box-flex: 1;
  -webkit-flex: 1;
  -ms-flex: 1;
  flex: 1;
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

.qsb-header {
  position: absolute;
  left: 0%;
  top: 0%;
  right: 0%;
  bottom: auto;
  z-index: 10;
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  height: 50px;
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
  background-color: rgba(42, 46, 57, 0.7);
  -webkit-backdrop-filter: blur(5px);
  backdrop-filter: blur(5px);
  color: #fff;
  font-size: 13px;
  font-weight: 400;
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
  -webkit-transition: all 300ms ease-in-out;
  transition: all 300ms ease-in-out;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Fira Sans', 'Droid Sans', 'Helvetica Neue', sans-serif;
  font-size: 12px;
}

.toolbar {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  height: 7vh;
  padding-right: 0.5rem;
  padding-left: 0.5rem;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-bottom: 1px solid #434651;
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
  -webkit-transition: all 300ms ease-in-out;
  transition: all 300ms ease-in-out;
  color: #adadad;
  text-align: center;
  white-space: nowrap;
}

.button:hover {
  background-color: rgba(255, 255, 255, 0.05);
}

.button.w--current {
  background-color: #1b72e3;
  color: #fff;
}

.button.middle {
  margin-right: 6px;
  margin-left: 6px;
}

.connection-info {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  padding-right: 1rem;
  padding-left: 1rem;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  color: #00ad6b;
}

.status-circle {
  width: 8px;
  height: 8px;
  margin-right: 8px;
  border-radius: 100%;
  background-color: #00ad6b;
}

.large-trade-grid {
  width: 100%;
  justify-content: space-between;
  align-items: center;
  align-content: center;
  grid-column-gap: 16px;
  grid-row-gap: 0px;
  grid-template-areas: "Area Area-2";
  grid-template-columns: max-content 1fr;
  grid-template-rows: auto;
}

.symbol-pairs-long {
  color: rgba(209, 212, 220, 0.6);
}

.value-neutral {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: end;
  -webkit-justify-content: flex-end;
  -ms-flex-pack: end;
  justify-content: flex-end;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 4px;
  color: white;
}
.value-increase {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: end;
  -webkit-justify-content: flex-end;
  -ms-flex-pack: end;
  justify-content: flex-end;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 4px;
  color: #00ad6b;
}

.value-decrease {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: end;
  -webkit-justify-content: flex-end;
  -ms-flex-pack: end;
  justify-content: flex-end;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 4px;
  color: #d9475a;
}

@media screen and (max-width: 991px) {
  .hotbar {
    -webkit-box-orient: horizontal;
    -webkit-box-direction: normal;
    -webkit-flex-direction: row;
    -ms-flex-direction: row;
    flex-direction: row;
    border-top: 1px solid #434651;
  }
}

@media screen and (max-width: 767px) {
  .hotbar {
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
    -webkit-flex-direction: column;
    -ms-flex-direction: column;
    flex-direction: column;
  }
}

#w-node-b736b7d6-0c81-c102-1fde-dd42ddff419b-53bf46aa {
  -ms-grid-row: 1;
  -ms-grid-column: 1;
  -ms-grid-column-align: start;
  justify-self: start;
  grid-area: Area;
}

#w-node-_2c7ab8d7-3d94-eb89-3828-6f933102b1d1-53bf46aa {
  -ms-grid-row: 1;
  -ms-grid-column: 3;
  -ms-grid-column-align: end;
  justify-self: end;
  grid-area: Area-2;
}
</style>