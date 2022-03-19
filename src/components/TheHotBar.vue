<template>
  <div class="hotbar">
        <GreatestGainers />
        <GreatestLosers />
      </div>
</template>

<script>
import GreatestGainers from '../components/GreatestGainers.vue'
import GreatestLosers from '../components/GreatestLosers.vue'

export default {
    components: {
        GreatestGainers,
        GreatestLosers,
    }

}
</script>

<style>
.tg-item {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  height: 40px;
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
  font-size: 12px;
  color: #d1d4dc;
}

.tg-item:nth-child(even)
{
  background: rgba(0, 0, 0, 0.1);
}

.item_listing-data {
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

.qs-block {
  position: relative;
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  height: 50vh;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -webkit-flex-direction: column;
  -ms-flex-direction: column;
  flex-direction: column;
}

.qs-block.losers {
  border-top: 5px none #d9475a;
  background-image: -webkit-gradient(linear, left top, right top, color-stop(50%, transparent), to(rgba(217, 71, 90, 0.09)));
  background-image: linear-gradient(90deg, transparent 50%, rgba(217, 71, 90, 0.09));
}

.qs-block.ad {
  padding-bottom: 0rem;
  border-top: 10px solid #16419d;
}

.qs-block.gainers {
  background-image: -webkit-gradient(linear, right top, left top, from(rgba(0, 173, 107, 0.09)), color-stop(50%, hsla(0, 0%, 100%, 0)));
  background-image: linear-gradient(270deg, rgba(0, 173, 107, 0.09), hsla(0, 0%, 100%, 0) 50%);
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
  opacity: 0.31;
  line-height: 18px;
  text-transform: uppercase;
}

.price_value {
  color: #white;
}

.asset_icon {
  width: 16px;
  height: 16px;
  margin-right: 10px;
  border-radius: 100%;
}

.lottie-animation {
  width: 32px;
  height: 32px;
  margin-right: 1rem;
  padding: 6px;
  border-radius: 8px;
  background-color: #101219;
}

.qsb-header {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  padding: 1rem;
  -webkit-box-pack: justify;
  -webkit-justify-content: space-between;
  -ms-flex-pack: justify;
  justify-content: space-between;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  border-bottom: 1px solid #434651;
  background-color: #1c1e29;
  color: #fff;
  font-size: 13px;
  font-weight: 400;
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

.ad-logo {
  margin-right: 1rem;
  padding: 6px;
  border-radius: 10px;
  background-color: #101219;
}

.image-4 {
  height: 18px;
  color: #a7b0c2;
}

.qsbh-icon {
  width: 24px;
  height: 24px;
}

.price_percent-change-negative {
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
  background-size: 12px;
  background-repeat: no-repeat;
  color: #d9475a;
}

.sidebar {
  width: 230px;
  background-color: #1c1e29;
  outline-color: #434651;
  outline-offset: 0px;
  outline-style: solid;
  outline-width: 1px;
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

.asset_name {
  margin-right: 4px;
  line-height: 18px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.item_asset-data {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  width: 130px;
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
</style>