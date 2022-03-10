<template>
  <div class="app">
    <TheMarketBanner />
    <TheNavigation />
    <router-view/>
  </div>
</template>

<script>
import TheMarketBanner from '@/components/TheMarketBanner.vue'
import TheNavigation from '@/components/TheNavigation.vue'


export default {
  components: {
    TheMarketBanner,
    TheNavigation
  }
}
</script>



<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.app {
  font-size: 12px;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Fira Sans', 'Droid Sans', 'Helvetica Neue', sans-serif;
  background: #f5f6f9;
  padding-bottom: 4rem;
}

.navigation {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  max-width: 1368px;
  margin-right: auto;
  margin-left: auto;
  padding-top: 1.2rem;
  padding-bottom: 1.2rem;
  -webkit-box-pack: justify;
  -webkit-justify-content: space-between;
  -ms-flex-pack: justify;
  justify-content: space-between;
}

.left-content {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
}

.logo {
  height: 28px;
  margin-right: 8px;
}

.navigation-block {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  padding-left: 20px;
}

.dropdown-link {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  height: 32px;
  padding-right: 0.8rem;
  padding-left: 0.8rem;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 4px;
  -webkit-transition: background-color 300ms ease-in-out;
  transition: background-color 300ms ease-in-out;
  font-weight: 500;
  cursor: pointer;
}

.dropdown-link:hover {
  background-color: #e9ebf1;
}

.logo-wrapper {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  height: 32px;
  padding-right: 20px;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
  -webkit-flex-direction: row;
  -ms-flex-direction: row;
  flex-direction: row;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-right: 1px solid #e3e4e9;
}

.logo-text {
  font-family: Montserrat, sans-serif;
  color: #7b849b;
  font-size: 14px;
  line-height: 21px;
  font-weight: 600;
  letter-spacing: 1px;
  text-transform: uppercase;
}

.dropdown-text {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  padding-right: 24px;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  background-image: url('./assets/images/dd-arrow-dblue.svg');
  background-position: 100% 50%;
  background-size: 16px;
  background-repeat: no-repeat;
  line-height: 14px;
}

.right-content {
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
}

.utilities-wrapper {
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
}

.dark-mode-button {
  width: 32px;
  height: 32px;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 4px;
  background-image: url('./assets/images/moon.png');
  background-position: 50% 50%;
  background-size: 18px;
  background-repeat: no-repeat;
  -webkit-transition: background-color 300ms ease-in-out;
  transition: background-color 300ms ease-in-out;
  cursor: pointer;
}

.dark-mode-button:hover {
  background-color: #e9ebf1;
}

.language-button {
  width: 32px;
  height: 32px;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 4px;
  background-image: url('./assets/images/language.png');
  background-position: 50% 50%;
  background-size: 18px;
  background-repeat: no-repeat;
  -webkit-transition: background-color 300ms ease-in-out;
  transition: background-color 300ms ease-in-out;
  cursor: pointer;
}

.language-button:hover {
  background-color: #e9ebf1;
}

.divider {
  width: 1px;
  height: 32px;
  margin-right: 0.8rem;
  margin-left: 0.8rem;
  background-color: #e2e4e8;
}

.divider.darker {
  background-color: #c9cbd1;
}

.search-wrapper {
  position: relative;
}

.search-input {
  margin-bottom: 0px;
  padding-left: 40px;
  border: 1px none #000;
  border-radius: 4px;
  background-color: #f5f6f9;
  background-image: url('./assets/images/search.svg');
  background-position: 12px 50%;
  background-size: 18px;
  background-repeat: no-repeat;
}

.search-input::-webkit-input-placeholder {
  color: #c9cfdd;
}

.search-input:-ms-input-placeholder {
  color: #c9cfdd;
}

.search-input::-ms-input-placeholder {
  color: #c9cfdd;
}

.search-input::placeholder {
  color: #c9cfdd;
}

.search-block {
  margin-bottom: 0px;
  margin-left: 1rem;
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
  background-color: #c9cfdd;
  color: #fff;
  font-size: 11px;
  font-weight: 600;
}

.divider-transparent {
  width: 1px;
  height: 32px;
  margin-right: 0.8rem;
  margin-left: 0.8rem;
}

.market-statistics-block {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  margin-right: 1.2rem;
  padding-top: 0.8rem;
  padding-bottom: 0.8rem;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
  -webkit-flex-direction: row;
  -ms-flex-direction: row;
  flex-direction: row;
}

.value-text {
  color: hsla(0, 0%, 100%, 0.75);
  font-weight: 500;
}

.muted-text {
  color: #5d667b;
  font-size: 12px;
}

.muted-text.margin-right {
  margin-right: 6px;
  color: rgba(255, 255, 255, 0.6);
  font-weight: 400;
}

.ms-wrapper {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  max-width: 1368px;
  margin-right: auto;
  margin-left: auto;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
}

.pt-wrapper {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  max-width: 1368px;
  margin-right: auto;
  margin-left: auto;
  padding: 1.2rem 1rem;
  -webkit-box-pack: justify;
  -webkit-justify-content: space-between;
  -ms-flex-pack: justify;
  justify-content: space-between;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
}

.toolbar-button {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  height: 32px;
  padding-right: 0.8rem;
  padding-left: 0.8rem;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 4px;
  -webkit-transition: background-color 300ms ease-in-out;
  transition: background-color 300ms ease-in-out;
  text-transform: capitalize;
  cursor: pointer;
}

.toolbar-button:hover {
  background-color: #e9ebf1;
}

.toolbar-button.active:hover {
  background-color: #d3d7e0;
}

.pt-left {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
}

.pt-right {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
}

.category-text {
  margin-right: 0.8rem;
  color: #58667e;
  line-height: 14px;
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

.selector-button {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  margin-right: 0.6rem;
  padding: 0.8rem 1.2rem;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 4px;
  background-color: #f5f6f9;
  -webkit-transition: background-color 300ms ease-in-out;
  transition: background-color 300ms ease-in-out;
  color: #323c52;
  font-size: 12px;
  line-height: 12px;
  font-weight: 500;
  cursor: pointer;
}

.selector-button:hover {
  background-color: #d5d9e4;
}

.selector-button.active {
  background-color: #1b72e3;
  color: #fff;
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
  color: #5d667b;
  font-size: 8px;
  line-height: 10px;
  font-weight: 600;
  letter-spacing: 1px;
  text-transform: uppercase;
}

.asset-logo {
  width: 21px;
  height: 21px;
  margin-right: 10px;
  border-radius: 100%;
}

.table-row {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  padding: 1rem;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-style: none none solid;
  border-width: 1px 1px 1px 3px;
  border-color: rgba(229, 230, 236, 0.1) #2a2e41 #f5f6f9 #fff;
}

.table-heading-text {
  color: #5d667b;
  font-size: 10px;
  font-weight: 600;
  text-transform: uppercase;
}

.value {
  color: #1e293b;
  font-size: 12px;
  line-height: 18px;
  font-weight: 600;
}

.value.assets-name {
  margin-right: 6px;
  font-size: 13px;
  font-weight: 600;
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
  background-color: rgba(232, 235, 240, 0.6);
  color: #485063;
  font-size: 10px;
  line-height: 12px;
}

.value-muted {
  padding-right: 18px;
  color: #7b849b;
  font-size: 12px;
  line-height: 18px;
}

.value-muted.positive {
  background-image: url('./assets/images/increase-icon.svg');
  background-position: 100% 50%;
  background-size: 10px;
  background-repeat: no-repeat;
  color: #00ad6b;
  font-size: 11px;
  font-weight: 600;
}

.supply-bar-wrapper {
  width: 140px;
  height: 4px;
  margin-top: 4px;
  border-radius: 25px;
  background-color: #e9ebf1;
}

.supply {
  width: 90.36%;
  height: 100%;
  border-radius: 25px;
  background-color: #1c71e2;
}


.accounts-component {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: end;
  -webkit-justify-content: flex-end;
  -ms-flex-pack: end;
  justify-content: flex-end;
}

.button {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  height: 32px;
  padding-right: 0.8rem;
  padding-left: 0.8rem;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 4px;
  -webkit-transition: all 300ms ease-in-out;
  transition: all 300ms ease-in-out;
  color: #000;
  font-weight: 500;
  cursor: pointer;
}

.button:hover {
  background-color: #e9ebf1;
}

.smart-table {
  position: relative;
  max-width: 1368px;
  margin-right: auto;
  margin-left: auto;
  background-color: #fff;
}

.rank {
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
  background-color: #f2f3f6;
  font-size: 12px;
  line-height: 12px;
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

.cell.xl {
  width: 180px;
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

.cell.l {
  width: 120px;
}

.cell.rank {
  width: 60px;
  -webkit-box-align: start;
  -webkit-align-items: flex-start;
  -ms-flex-align: start;
  align-items: flex-start;
  background-color: transparent;
}

.volatility-wrap {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -webkit-flex-direction: column;
  -ms-flex-direction: column;
  flex-direction: column;
  -webkit-box-pack: justify;
  -webkit-justify-content: space-between;
  -ms-flex-pack: justify;
  justify-content: space-between;
  -webkit-box-align: end;
  -webkit-align-items: flex-end;
  -ms-flex-align: end;
  align-items: flex-end;
  line-height: 14px;
}

.volatility-value {
  line-height: 18px;
  font-weight: 600;
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

.table-head {
  position: -webkit-sticky;
  position: sticky;
  top: 76px;
  z-index: 100;
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  max-width: 1368px;
  margin-right: auto;
  margin-left: auto;
  padding: 1rem;
  -webkit-box-align: stretch;
  -webkit-align-items: stretch;
  -ms-flex-align: stretch;
  align-items: stretch;
  border-top: 1px solid #eaebf1;
  border-bottom: 1px solid #eaebf1;
  background-color: hsla(0, 0%, 100%, 0.75);
  -webkit-backdrop-filter: blur(5px);
  backdrop-filter: blur(5px);
}

.change-wrap {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -webkit-flex-direction: column;
  -ms-flex-direction: column;
  flex-direction: column;
  -webkit-box-pack: justify;
  -webkit-justify-content: space-between;
  -ms-flex-pack: justify;
  justify-content: space-between;
  -webkit-box-align: end;
  -webkit-align-items: flex-end;
  -ms-flex-align: end;
  align-items: flex-end;
  border-radius: 4px;
}

.volatility-bar-wrapper {
  width: 91px;
  height: 4px;
  margin-top: 5px;
  border-radius: 25px;
  background-color: #e8ebf0;
}

.volatility {
  width: 84%;
  height: 100%;
  border-radius: 25px;
  background-color: #82a9e4;
}

.change-pct-value-positive {
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
  background-image: url('./assets/images/arrow-up-right.svg');
  background-position: 100% 50%;
  background-size: 13px;
  background-repeat: no-repeat;
  color: #00ad6b;
  font-weight: 600;
}

.table-toolbar {
  position: -webkit-sticky;
  position: sticky;
  top: 0px;
  z-index: 100;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
  background-color: hsla(0, 0%, 100%, 0.75);
  box-shadow: none;
  -webkit-backdrop-filter: blur(5px);
  backdrop-filter: blur(5px);
}

.change-pct-value-negative {
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
  background-image: url('./assets/images/arrow-down-right.svg');
  background-position: 100% 50%;
  background-size: 13px;
  background-repeat: no-repeat;
  color: #d9475a;
  font-weight: 600;
}

.quick-statistics {
  display: -ms-grid;
  display: grid;
  max-width: 1368px;
  margin-right: auto;
  margin-left: auto;
  -webkit-box-pack: start;
  -webkit-justify-content: flex-start;
  -ms-flex-pack: start;
  justify-content: flex-start;
  grid-auto-columns: 1fr;
  grid-column-gap: 16px;
  grid-row-gap: 16px;
  -ms-grid-columns: auto auto auto auto;
  grid-template-columns: auto auto auto auto;
  -ms-grid-rows: auto;
  grid-template-rows: auto;
}

.qs-block {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  padding: 1rem;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -webkit-flex-direction: column;
  -ms-flex-direction: column;
  flex-direction: column;
  border-radius: 4px;
  background-color: #fff;
  box-shadow: 1px 1px 3px 0 rgba(0, 0, 0, 0.1);
}

.qs-title {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  margin-bottom: 10px;
  padding-right: 40px;
  -webkit-box-pack: justify;
  -webkit-justify-content: space-between;
  -ms-flex-pack: justify;
  justify-content: space-between;
  font-size: 12px;
  font-weight: 600;
}

.tg-item {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  height: 32px;
  -webkit-box-pack: start;
  -webkit-justify-content: flex-start;
  -ms-flex-pack: start;
  justify-content: flex-start;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
}

.item_asset-data {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  width: 160px;
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

.item_price-data {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  width: 80px;
  -webkit-box-pack: end;
  -webkit-justify-content: flex-end;
  -ms-flex-pack: end;
  justify-content: flex-end;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
}

.price_value {
  color: #1e293b;
  font-size: 12px;
  line-height: 18px;
  font-weight: 500;
}

.price_percent-change-positive {
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
  background-image: url('./assets/images/arrow-up-right.svg');
  background-position: 100% 50%;
  background-size: 13px;
  background-repeat: no-repeat;
  color: #00ad6b;
  font-weight: 600;
}

.asset_icon {
  width: 18px;
  height: 18px;
  margin-right: 10px;
  border-radius: 100%;
}

.asset_name {
  margin-right: 6px;
  color: #1e293b;
  font-size: 12px;
  line-height: 18px;
  font-weight: 500;
}

.asset_ticker {
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
  color: #5d667b;
  font-size: 8px;
  line-height: 10px;
  font-weight: 500;
  letter-spacing: 1px;
  text-transform: uppercase;
}

.item_rank {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  width: 20px;
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
  -webkit-box-align: start;
  -webkit-align-items: flex-start;
  -ms-flex-align: start;
  align-items: flex-start;
}

.rank_value {
  color: #1e293b;
  font-size: 12px;
  line-height: 18px;
  font-weight: 400;
}

.item_listing-data {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  width: 90px;
  -webkit-box-pack: end;
  -webkit-justify-content: flex-end;
  -ms-flex-pack: end;
  justify-content: flex-end;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
}

.listing_added {
  color: #7b849b;
  font-size: 12px;
  line-height: 18px;
  font-weight: 400;
}

.sponsor-info {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  margin-bottom: 10px;
  background-image: url('./assets/images/sponsored.png');
  background-position: 100% 50%;
  background-size: contain;
  background-repeat: no-repeat;
}

.image-2 {
  padding-right: 10px;
}

.sponser-button {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  height: 32px;
  padding-right: 0.8rem;
  padding-left: 0.8rem;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-radius: 4px;
  background-color: #1c71e2;
  -webkit-transition: background-color 300ms ease-in-out;
  transition: background-color 300ms ease-in-out;
  color: #fff;
  font-size: 12px;
  line-height: 12px;
  font-weight: 500;
  cursor: pointer;
}

.sponser-button:hover {
  background-color: #d5d9e4;
}

.text-block-2 {
  padding-top: 4px;
}

.sponsor-name {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  padding-right: 40px;
  -webkit-box-pack: justify;
  -webkit-justify-content: space-between;
  -ms-flex-pack: justify;
  justify-content: space-between;
  font-size: 12px;
  font-weight: 600;
}

.navigation_component {
  background-color: #fff;
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1);
}

.highlights_component {
  padding-top: 2rem;
  padding-bottom: 2rem;
}

.market-banner_component {
  background-color: #1e293b;
}

.layout-1368 {
  max-width: 1368px;
  margin-right: auto;
  margin-left: auto;
}

.table {
  border-radius: 4px;
  box-shadow: 1px 1px 3px 0 rgba(0, 0, 0, 0.1);
}

.text-block-3 {
  color: #1e293b;
  font-size: 14px;
  font-weight: 600;
}

#w-node-e2ccbdc9-fd14-c110-6bd1-dc7efa6701cd-d98399a7 {
  -ms-grid-column: span 1;
  grid-column-start: span 1;
  -ms-grid-column-span: 1;
  grid-column-end: span 1;
  -ms-grid-row: span 1;
  grid-row-start: span 1;
  -ms-grid-row-span: 1;
  grid-row-end: span 1;
}

#w-node-a40b5b2b-53c7-5367-1ddf-c8201bb03b97-d98399a7 {
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
