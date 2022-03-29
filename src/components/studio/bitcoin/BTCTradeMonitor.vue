<template>
  <div id="w-node-_3bd34822-0d8a-5a2c-c08e-9eaa199a0919-cd1d760e" class="studio-div-wrapper">
          <div class="header-wrap">
            <div class="studio-table-header">
              <div>Exchange Trade Monitor</div>
              <div class="utility-wrap">
                <select @change="e => $emit('input', e.target.tradeFilter)" v-model="tradeFilter" id="field" name="field" data-name="Field" class="select-filter">
                  <option :value="0">No Filter</option>
                  <option :value="1000">> 1,000</option>
                  <option :value="5000">> 5,000</option>
                  <option :value="10000">> 10,000</option>
                  <option :value="20000">> 20,000</option>
                  <option :value="30000">> 30,000</option>
                  <option :value="40000">> 40,000</option>
                  <option :value="50000">> 50,000</option>
                  <option :value="100000">> 100,000</option>
                  <option :value="250000">> 250,000</option>
                  <option :value="500000">> 500,000</option>
                  <option :value="1000000">> 1,000,000</option>
                </select>
                <select v-model="tradeFilter" id="field" name="field" data-name="Field" class="select-filter">
                  <option :value="0">No Filter</option>
                  <option :value="1000">> 1,000</option>
                  <option :value="5000">> 5,000</option>
                  <option :value="10000">> 10,000</option>
                  <option :value="20000">> 20,000</option>
                  <option :value="30000">> 30,000</option>
                  <option :value="40000">> 40,000</option>
                  <option :value="50000">> 50,000</option>
                  <option :value="100000">> 100,000</option>
                  <option :value="250000">> 250,000</option>
                  <option :value="500000">> 500,000</option>
                  <option :value="1000000">> 1,000,000</option>
                </select>
              </div>
            </div>
            <div class="table-head">
              <div class="cell small">
                <div class="table-heading-text">Time</div>
              </div>
              <div class="cell small">
                <div class="table-heading-text">Type</div>
              </div>
              <div class="cell small">
                <div class="table-heading-text">Symbol</div>
              </div>
              <div class="cell large">
                <div class="table-heading-text">Exchange</div>
              </div>
              <div class="cell justify-right">
                <div class="table-heading-text">Trade Value</div>
              </div>
              <div class="cell justify-right">
                <div class="table-heading-text">Spot</div>
              </div>
              <div class="cell justify-right">
                <div class="table-heading-text">Quantity</div>
              </div>
              <div class="cell justify-right">
                <div class="table-heading-text">Trade ID</div>
              </div>
            </div>
          </div>
          <div class="table-row" v-for="(data) in filteredTrades.slice().reverse()" :key="data" :class="tradeDivStyler(data.m)">
            <div class="cell small">
              <div class="muted-value">{{ dateTime(data.E) }}</div>
            </div>
            <div class="cell small middle">
              <div class="buy-badge" :class="tradeDivStyler(data.m)" :key="data.m">{{ data.m }}</div>
            </div>
            <div class="cell small">
              <div class="value assets-name">BTCUSD</div>
            </div>
            <div class="cell large">
              <div class="muted-value">Binance USD-M Futures</div>
            </div>
            <div class="cell justify-right">
              <div class="trade-value">${{ Math.floor(data.p * data.q).toLocaleString() }}</div>
            </div>
            <div class="cell justify-right">
              <div class="muted-value">${{ data.p }}</div>
            </div>
            <div class="cell justify-right">
              <div class="muted-value">{{ data.q }} BTC</div>
            </div>
            <div class="cell justify-right">
              <div class="value muted-value">{{ data.t }}</div>
            </div>
          </div>
        </div>
</template>

<script>
import moment from 'moment'

export default {

    components: {
    },

    created() {
        this.getBinanceSpot();
        this.moment = moment;
    },

    data: () => ({
        errors: [],
        isMarketMaker: true,
        tradeFilter: 0,
        connection: null,
        tradeDataList: [],
    }),

    computed: {
      filteredTrades() {
              return this.tradeDataList.filter(data => Math.floor(data.p * data.q) > this.tradeFilter);
      }
    },

    methods: {

        getBinanceSpot() {
          console.log("Starting connection to WebSocket Server");
          this.connection = new WebSocket("wss://stream.binance.com:9443/ws/btcusdt@trade");

          this.connection.addEventListener("message", (event) => {

            let tradeDataString = event.data;

            let parsedData = JSON.parse(tradeDataString);
            
            // push new item to array
            this.tradeDataList.push(parsedData);
            
            // keep only last 10
            this.tradeDataList = this.tradeDataList.slice(Math.max(this.tradeDataList.length - 250, 0))
          });

          this.connection.onopen = function(event) {
            console.log(event);
            console.log("Successfully connected to the echo websocket server...");
          };
        },

        tradeDivStyler(value) { 
            return {
            'market-maker': value === true,
            'market-taker': value === false
          };
        },

        tradeBadgeStyler(value) { 
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

        dateTime(value) {
          return moment(value).format('h:mm:ss a');
        },

    },

}
</script>


<style scoped>
.table-row {
  display: flex;
  padding-top: 0.6rem;
  padding-right: 1rem;
  padding-bottom: 0.6rem;
  padding-left: 1rem;
  align-items: center;
  border-bottom-style: solid;
  border-bottom-width: 1px;
  border-bottom-color: hsla(230.7692307692308, 18.84%, 13.53%, 1.00);
}  
.market-maker {
  background-color: hsla(157, 100%, 34%, 0.1);
  animation: flashbuy 0.5s ease-out 1;
}
  @keyframes flashbuy {
    0% {
      background-color: hsla(157, 100%, 34%, 0.25);
    }
  }
.market-taker {
    background-color: hsla(352, 66%, 56%, 0.1);
    animation: flashsell 0.5s ease-out 1;
}
  @keyframes flashsell {
    0% {
      background-color: hsla(352, 66%, 56%, 0.25);
    }
  }

.utility-wrap {
  display: flex;
}
.studio-div-wrapper {
  position: relative;
  overflow: scroll;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #434651;
}

.Block:local-styles {
  grid-area: Trades;
}

.header-wrap {
  position: sticky;
  top: 0px;
}

.studio-table-header {
  display: flex;
  height: 50px;
  padding-right: 1rem;
  padding-left: 1rem;
  justify-content: space-between;
  align-items: center;
  border-bottom-style: solid;
  border-bottom-width: 1px;
  border-bottom-color: #434651;
  background-color: rgba(42, 46, 57, 0.7);
  backdrop-filter: blur(5px);
  color: white;
  font-size: 13px;
}

.select-filter {
  width: 123px;
  margin-bottom: 0px;
  padding-top: 9px;
  padding-right: 1rem;
  padding-bottom: 9px;
  padding-left: 1rem;
  border-top-style: none;
  border-top-width: 1px;
  border-top-color: black;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: black;
  border-bottom-style: none;
  border-bottom-width: 1px;
  border-bottom-color: black;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: black;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
  background-color: transparent;
  opacity: 0.6;
  color: hsla(0, 0.00%, 100.00%, 1.00);
  font-size: 12px;
}

.table-head {
  position: sticky;
  top: 0px;
  z-index: 10;
  display: flex;
  overflow: hidden;
  padding-top: 0.6rem;
  padding-right: 1rem;
  padding-bottom: 0.6rem;
  padding-left: 1rem;
  align-items: center;
  border-bottom-style: solid;
  border-bottom-width: 1px;
  border-bottom-color: #434651;
  background-color: hsla(224, 15.15%, 19.41%, 0.25);
  box-shadow: none
    /* 0 14px 18px 0 hsla(0, 0.00%, 0.00%, 0.10) */
  ;
  backdrop-filter: blur(5px);
  color: #d1d4dc;
  font-size: 10px;
  font-weight: 400;
  text-transform: capitalize;
}

.cell {
  display: flex;
  width: 120px;
  height: 100%;
  flex-direction: row;
  justify-content: flex-start;
  align-items: flex-start;
  flex-grow: 1;
  flex-shrink: 1;
  flex-basis: 0%;
}

.cell.small {
  width: 90px;
  flex-grow: 0;
  flex-shrink: 1;
  flex-basis: auto;
}

.cell.large {
  width: 160px;
  flex-direction: column;
  flex-grow: 0;
  flex-shrink: 1;
  flex-basis: auto;
}

.cell.justify-right {
  justify-content: flex-end;
  align-items: center;
}

.muted-value {
  color: rgba(209, 212, 220, 0.6);
}

.buy-badge {
  padding-top: 4px;
  padding-right: 8px;
  padding-bottom: 4px;
  padding-left: 8px;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
  background-color: hsla(157.1098265895954, 100.00%, 33.92%, 0.30);
  color: white;
  font-size: 10px;
  line-height: 14px;
  font-weight: 700;
  letter-spacing: 0px;
}

.value.assets-name {
  margin-right: 6px;
  font-weight: 600;
}
</style>