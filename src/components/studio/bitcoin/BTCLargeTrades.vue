<template>
<div id="w-node-_0ece904f-6af7-035e-2c91-54e08e1e8f3e-cd1d760e" class="large-trade-monitor">
          <div class="monitor-header">
            <div>Large Trade Monitor</div>
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
          </div>
          <div class="monitor-items">
            <div class="monitor-item" v-for="(data) in filteredTrades.slice().reverse()" :key="data.id" :class="tradeDivStyler(data.m)">
              <div id="large-trade-grid" class="w-layout-grid monitor-row">
                <div id="w-node-_9e4cabd2-3d97-695d-80de-b01946603ae1-cd1d760e" class="data-cell">
                  <div class="text">Bitcoin / TetherUS</div>
                  <div id="w-node-_9e4cabd2-3d97-695d-80de-b01946603ae4-cd1d760e" class="muted-text">Binance.com</div>
                  <div class="muted-text small">{{ dateTime(data.E) }}</div>
                </div>
                <div id="w-node-_9e4cabd2-3d97-695d-80de-b01946603ae8-cd1d760e" class="data-cell-right">
                  <div class="quoteprice">${{ Math.floor(data.p * data.q).toLocaleString() }}</div>
                  <div class="muted-text">{{ data.q }} BTC</div>
                </div>
              </div>
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
        this.getTradeStream();
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

        getTradeStream() {
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
          return moment(value).format('MMMM Do YYYY, h:mm:ss a');
        },

    },

}
</script>


<style scoped>
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
.large-trade-monitor {
  position: relative;
  overflow: scroll;
  border-left-style: solid;
  border-left-width: 1px;
  border-left-color: #434651;
}

.Block:local-styles {
  grid-area: Widgets;
}

.monitor-header {
  position: sticky;
  top: 0px;
  display: flex;
  height: 50px;
  padding-right: 1rem;
  padding-left: 1rem;
  justify-content: space-between;
  align-items: center;
  border-bottom-style: solid;
  border-bottom-width: 1px;
  border-bottom-color: hsla(227.14285714285714, 9.46%, 29.02%, 1.00);
  background-color: rgba(42, 46, 57, 0.7);
  backdrop-filter: blur(5px);
  color: white;
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

.monitor-item {
  padding-top: 0.6rem;
  padding-right: 1rem;
  padding-bottom: 0.6rem;
  padding-left: 1rem;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: hsla(230.7692307692308, 18.84%, 13.53%, 1.00);
}

.monitor-item.buy {
  background-color: hsla(157.1098265895954, 100.00%, 33.92%, 0.10);
}

.monitor-row {
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

.data-cell {
  justify-content: flex-end;
  align-items: center;
}

.Block:local-styles {
  justify-self: start;
  grid-area: Area;
}

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

.Block:local-styles {
  grid-area: Area-3;
}

.quoteprice {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
  color: white;
}

#w-node-_9e4cabd2-3d97-695d-80de-b01946603ae8-cd1d760e {
  -ms-grid-row: 1;
  -ms-grid-column: 3;
  -ms-grid-column-align: end;
  justify-self: end;
  grid-area: Area-2;
}
</style>