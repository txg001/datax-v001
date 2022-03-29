<template>
  <div class="studio-template">
    <div class="studio-toolbar">
      <div class="studio-header">Bitcoin Studio</div>
      <a href="#" class="studio-button w-button">USD</a>
    </div>
    <div class="studio-main">
      <div class="w-layout-grid grid">
        <TradingViewChart />
        <BTCTradeMonitor />
        <BTCLargeTrades />
      </div>
    </div>
  </div>
</template>

<script>
import BTCLargeTrades from "../components/studio/bitcoin/BTCLargeTrades.vue";
import BTCTradeMonitor from "../components/studio/bitcoin/BTCTradeMonitor.vue";
import TradingViewChart from "../components/studio/bitcoin/TradingViewChart.vue";

export default {
  name: 'app',
  components: { BTCLargeTrades, BTCTradeMonitor, TradingViewChart },
  data() {
    return {
  
    }
  }
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

.body {
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
  background-color: #000;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Fira Sans', 'Droid Sans', 'Helvetica Neue', sans-serif;
}

.studio-template {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  width: 100%;
  height: 100vh;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -webkit-flex-direction: column;
  -ms-flex-direction: column;
  flex-direction: column;
  border-right: 1px solid #434651;
  border-left: 1px solid #434651;
  background-color: #1c1e29;
  color: #d1d4dc;
  font-size: 12px;
}

.studio-toolbar {
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
  background-color: rgba(42, 46, 57, 0.5);
  color: #fff;
  font-size: 14px;
}

.studio-main {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  height: 93vh;
  padding: 0rem;
}

.studio-button {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  margin-left: 12px;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 4px;
  background-color: rgba(255, 255, 255, 0.1);
  color: #adadad;
  text-align: center;
  white-space: nowrap;
}

.studio-button.w--current {
  background-color: #1b72e3;
  color: #fff;
}

.grid {
  -webkit-box-flex: 1;
  -webkit-flex: 1;
  -ms-flex: 1;
  flex: 1;
  grid-column-gap: 0px;
  grid-row-gap: 0px;
  grid-template-areas: "Chart-Data Widgets"
    "Trades Trades";
  -ms-grid-columns: 1fr 0px 350px;
  grid-template-columns: 1fr 350px;
  -ms-grid-rows: 1fr 0px 1fr;
  grid-template-rows: 1fr 1fr;
}

.studio-div-wrapper {
  position: relative;
  overflow: scroll;
  border-top: 1px solid #434651;
}

.cell {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  width: 120px;
  height: 100%;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
  -webkit-flex-direction: row;
  -ms-flex-direction: row;
  flex-direction: row;
  -webkit-box-pack: start;
  -webkit-justify-content: flex-start;
  -ms-flex-pack: start;
  justify-content: flex-start;
  -webkit-box-align: start;
  -webkit-align-items: flex-start;
  -ms-flex-align: start;
  align-items: flex-start;
  -webkit-box-flex: 1;
  -webkit-flex: 1;
  -ms-flex: 1;
  flex: 1;
}

.cell.justify-right {
  -webkit-box-pack: end;
  -webkit-justify-content: flex-end;
  -ms-flex-pack: end;
  justify-content: flex-end;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
}

.cell.large {
  width: 160px;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -webkit-flex-direction: column;
  -ms-flex-direction: column;
  flex-direction: column;
  -webkit-box-flex: 0;
  -webkit-flex: 0 auto;
  -ms-flex: 0 auto;
  flex: 0 auto;
}

.cell.small {
  width: 90px;
  -webkit-box-flex: 0;
  -webkit-flex: 0 auto;
  -ms-flex: 0 auto;
  flex: 0 auto;
}

.table-head {
  position: -webkit-sticky;
  position: sticky;
  top: 0px;
  z-index: 10;
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  overflow: hidden;
  padding: 0.6rem 1rem;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
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

.value.assets-name {
  margin-right: 6px;
  font-weight: 600;
}

.table-row {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  padding: 0.6rem 1rem;
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

.table-row.nth {
  background-color: rgba(0, 0, 0, 0.15);
}

.buy-badge {
  padding: 4px 8px;
  border-radius: 4px;
  background-color: rgba(0, 173, 107, 0.3);
  color: #fff;
  font-size: 10px;
  line-height: 14px;
  font-weight: 700;
  letter-spacing: 0px;
}

.trade-value {
  font-weight: 600;
}

.muted-value {
  color: rgba(209, 212, 220, 0.6);
}

.studio-div-wrapper-copy {
  border-style: none;
  border-width: 1px;
  border-color: #434651;
  border-radius: 4px;
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

.quoteprice {
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
  color: #fff;
}

.form {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
}

.form-block {
  margin-bottom: 0px;
}

.monitor-row {
  width: 100%;
  -webkit-box-pack: justify;
  -webkit-justify-content: space-between;
  -ms-flex-pack: justify;
  justify-content: space-between;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  -webkit-align-content: center;
  -ms-flex-line-pack: center;
  align-content: center;
  grid-column-gap: 16px;
  grid-row-gap: 0px;
  grid-template-areas: "Area Area-2";
  -ms-grid-columns: -webkit-max-content 16px 1fr;
  -ms-grid-columns: max-content 16px 1fr;
  grid-template-columns: -webkit-max-content 1fr;
  grid-template-columns: max-content 1fr;
  -ms-grid-rows: auto;
  grid-template-rows: auto;
}

.data-cell-right {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
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

.select-filter {
  width: 123px;
  margin-bottom: 0px;
  padding: 9px 1rem;
  border: 1px none #000;
  border-radius: 4px;
  background-color: transparent;
  opacity: 0.6;
  color: #fff;
  font-size: 12px;
}

.text {
  color: #d1d4dc;
}

.muted-text {
  color: rgba(209, 212, 220, 0.6);
}

.muted-text.small {
  color: rgba(209, 212, 220, 0.5);
  font-size: 10px;
  line-height: 21px;
}

.studio-table-header {
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
}

.large-trade-monitor {
  position: relative;
  overflow: scroll;
  border-left: 1px solid #434651;
}

.monitor-header {
  position: -webkit-sticky;
  position: sticky;
  top: 0px;
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
}

.monitor-item {
  padding: 0.6rem 1rem;
  border-bottom: 2px solid #1c1e29;
}

.monitor-item.buy {
  background-color: rgba(0, 173, 107, 0.1);
}

.header-wrap {
  position: -webkit-sticky;
  position: sticky;
  top: 0px;
}

#w-node-_4b6f2c0c-8594-3d1f-d7c5-6e4e0d21c218-cd1d760e {
  -ms-grid-row: 1;
  -ms-grid-column: 1;
  grid-area: Chart-Data;
}

#w-node-_3bd34822-0d8a-5a2c-c08e-9eaa199a0919-cd1d760e {
  -ms-grid-row: 3;
  -ms-grid-column: 1;
  -ms-grid-column-span: 3;
  grid-area: Trades;
}

#w-node-_0ece904f-6af7-035e-2c91-54e08e1e8f3e-cd1d760e {
  -ms-grid-row: 1;
  -ms-grid-column: 3;
  grid-area: Widgets;
}

#w-node-_9e4cabd2-3d97-695d-80de-b01946603ae1-cd1d760e {
  -ms-grid-row: 1;
  -ms-grid-column: 1;
  -ms-grid-column-align: start;
  justify-self: start;
  grid-area: Area;
}

#w-node-_9e4cabd2-3d97-695d-80de-b01946603ae4-cd1d760e {
  grid-area: Area-3;
}

#w-node-_9e4cabd2-3d97-695d-80de-b01946603ae8-cd1d760e {
  -ms-grid-row: 1;
  -ms-grid-column: 3;
  -ms-grid-column-align: end;
  justify-self: end;
  grid-area: Area-2;
}

#w-node-_6f9b2b29-b049-d364-1fbd-fceea4fbf76b-cd1d760e {
  -ms-grid-row: 1;
  -ms-grid-column: 1;
  -ms-grid-column-align: start;
  justify-self: start;
  grid-area: Area;
}

#w-node-_6f9b2b29-b049-d364-1fbd-fceea4fbf76e-cd1d760e {
  grid-area: Area-3;
}

#w-node-_6f9b2b29-b049-d364-1fbd-fceea4fbf772-cd1d760e {
  -ms-grid-row: 1;
  -ms-grid-column: 3;
  -ms-grid-column-align: end;
  justify-self: end;
  grid-area: Area-2;
}

#w-node-a9b80560-ddb3-b7f4-a6a6-2c0d7a095aac-cd1d760e {
  -ms-grid-row: 1;
  -ms-grid-column: 1;
  -ms-grid-column-align: start;
  justify-self: start;
  grid-area: Area;
}

#w-node-a9b80560-ddb3-b7f4-a6a6-2c0d7a095aaf-cd1d760e {
  grid-area: Area-3;
}

#w-node-a9b80560-ddb3-b7f4-a6a6-2c0d7a095ab3-cd1d760e {
  -ms-grid-row: 1;
  -ms-grid-column: 3;
  -ms-grid-column-align: end;
  justify-self: end;
  grid-area: Area-2;
}

#w-node-_0bd6bb32-b40d-f05b-e141-be468c4bdec2-cd1d760e {
  -ms-grid-row: 1;
  -ms-grid-column: 1;
  -ms-grid-column-align: start;
  justify-self: start;
  grid-area: Area;
}

#w-node-_0bd6bb32-b40d-f05b-e141-be468c4bdec5-cd1d760e {
  grid-area: Area-3;
}

#w-node-_0bd6bb32-b40d-f05b-e141-be468c4bdec9-cd1d760e {
  -ms-grid-row: 1;
  -ms-grid-column: 3;
  -ms-grid-column-align: end;
  justify-self: end;
  grid-area: Area-2;
}

#w-node-f4bc06d3-d970-2784-65e4-32627ad58484-cd1d760e {
  -ms-grid-row: 1;
  -ms-grid-column: 1;
  -ms-grid-column-align: start;
  justify-self: start;
  grid-area: Area;
}

#w-node-f4bc06d3-d970-2784-65e4-32627ad58487-cd1d760e {
  grid-area: Area-3;
}

#w-node-f4bc06d3-d970-2784-65e4-32627ad5848b-cd1d760e {
  -ms-grid-row: 1;
  -ms-grid-column: 3;
  -ms-grid-column-align: end;
  justify-self: end;
  grid-area: Area-2;
}

#w-node-bf4f6c3b-816a-7267-97e2-e8338995fb66-cd1d760e {
  -ms-grid-row: 1;
  -ms-grid-column: 1;
  -ms-grid-column-align: start;
  justify-self: start;
  grid-area: Area;
}

#w-node-bf4f6c3b-816a-7267-97e2-e8338995fb69-cd1d760e {
  grid-area: Area-3;
}

#w-node-bf4f6c3b-816a-7267-97e2-e8338995fb6d-cd1d760e {
  -ms-grid-row: 1;
  -ms-grid-column: 3;
  -ms-grid-column-align: end;
  justify-self: end;
  grid-area: Area-2;
}

#w-node-_62ae60f7-1c22-d665-1611-f57c892f80d2-cd1d760e {
  -ms-grid-row: 1;
  -ms-grid-column: 1;
  -ms-grid-column-align: start;
  justify-self: start;
  grid-area: Area;
}

#w-node-_62ae60f7-1c22-d665-1611-f57c892f80d5-cd1d760e {
  grid-area: Area-3;
}

#w-node-_62ae60f7-1c22-d665-1611-f57c892f80d9-cd1d760e {
  -ms-grid-row: 1;
  -ms-grid-column: 3;
  -ms-grid-column-align: end;
  justify-self: end;
  grid-area: Area-2;
}
</style>