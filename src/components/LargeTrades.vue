<template>
  <div class="qs-block">
        <div class="qsb-header">
          <div class="qsb-header-left">
            <div>Large BTC Trades</div>
          </div><img src="images/last-24-hours-96_1last-24-hours-96.png" loading="lazy" alt="" class="qsbh-icon">
        </div>
        <div class="top-gainers">
          <div class="tg-item" v-for="trades in trades" :key="trades">
            <div class="w-layout-grid large-trade-grid">
              <div id="w-node-b736b7d6-0c81-c102-1fde-dd42ddff419b-53bf46aa" class="data-cell">
                <div class="price">BTCUSD</div>
                <div class="price">Bitcoin / TetherUS</div>
              </div>
              <div id="w-node-_2c7ab8d7-3d94-eb89-3828-6f933102b1d1-53bf46aa" class="data-cell">
                <div class="price">{{ trades.quoteQty }}</div>
                <div class="price">{{ trades.qty }} BTC</div>
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
    }),

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


    },

}
</script>

<style scoped>
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
  -webkit-transition: background-color 300ms ease-in-out;
  transition: background-color 300ms ease-in-out;
  color: #d1d4dc;
  cursor: pointer;
}

.tg-item:hover {
  background-color: hsla(0, 0%, 100%, 0.05);
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

.icon {
  width: 20px;
  height: 20px;
  margin-right: 0.8rem;
}

.icon.green {
  color: #00ad6b;
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
  grid-template-areas: "Area Area-2";
  -ms-grid-rows: auto;
  grid-template-rows: auto;
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
  -ms-grid-column-align: start;
  justify-self: start;
  -ms-grid-column: span 1;
  grid-column-start: span 1;
  -ms-grid-column-span: 1;
  grid-column-end: span 1;
  -ms-grid-row: span 1;
  grid-row-start: span 1;
  -ms-grid-row-span: 1;
  grid-row-end: span 1;
}

#w-node-_2c7ab8d7-3d94-eb89-3828-6f933102b1d1-53bf46aa {
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