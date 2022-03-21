<template>
  <div class="hotbar">
    
    


  <div class="toolbar">

          <select v-model="current" id="field" name="field" data-name="Field" class="select-field w-select">
            <option value="GreatestGainers">Top Movers</option>
            <option value="LargeTrades">Large Trades </option>
          </select>

      
      <div class="connection-info">
        <div class="status-circle"></div>
        <div>Connected</div>
      </div>
    </div>

    <div class="main-wrap">
      <keep-alive>
        <component :is="current"></component>
      </keep-alive>
    </div>
  </div>
</template>

<script>
import GreatestGainers from "./GreatestGainers.vue";
import LargeTrades from "./LargeTrades.vue";


export default {
  data() {
    return {
      current: 'GreatestGainers',
      isActive: true
    };
  },
  components: {
    GreatestGainers,
    LargeTrades
  },
}
</script>

<style scoped>
select {
    appearance: none !important;
    -webkit-appearance: none !important;
    -moz-appearance: none !important;
  }

  .w-select {
  display: block;
  width: 100%;
  height: 38px;
  padding: 8px 12px;
  margin-bottom: 10px;
  font-size: 14px;
  line-height: 1.428571429;
  color: #333333;
  vertical-align: middle;
  background-color: #ffffff;
  border: 1px solid #cccccc;
}

.select-field {
  margin-bottom: 0px;
  padding: 9px 1rem;
  border: 1px none #000;
  border-radius: 4px;
  background-color: hsla(0, 0%, 100%, 0.1);
  background-image: url('../assets/images/chevron-down-3.svg');
  background-position: 95% 50%;
  background-size: 12px;
  background-repeat: no-repeat;
  color: #fff;
  font-size: 12px;
}
.active.button.w-button {
  background-color: #1b72e3;
  color: white;
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
  background-color: #1c1e29;
  outline-color: #434651;
  outline-offset: 0px;
  outline-style: solid;
  outline-width: 1px;
}

.toolbar {
  display: flex;
  height: 7vh;
  padding-right: 1rem;
  padding-left: 1rem;
  align-items: center;
  border-bottom-style: solid;
  border-bottom-width: 1px;
  border-bottom-color: #434651;
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
  display: flex;
  justify-content: center;
  align-items: center;
  flex-grow: 1;
  flex-shrink: 1;
  flex-basis: 0%;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
  background-color: hsla(213.89999999999998, 0.00%, 100.00%, 0.10);
  transition-property: all;
  transition-duration: 300ms;
  transition-timing-function: ease-in-out;
  color: hsla(216, 0.00%, 68.00%, 1.00);
  text-align: center;
  white-space: nowrap;
}

.button:hover {
  background-color: hsla(213.89999999999998, 0.00%, 100.00%, 0.05);
}

.button.w--current {
  background-color: #1b72e3;
  color: #fff;
}

.button.middle {
  margin-right: 6px;
  margin-left: 6px;
}

.button.middle:focus {
  background: #1b72e3;
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
  animation: blinker 2s ease-in-out infinite;;
}
@keyframes blinker {
  50% {
    background-color: rgba(0, 173, 107, 0.25);
  }
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

</style>