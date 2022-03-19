<template>
  <div class="hotbar">
    <div class="toolbar">
      <a href="index.html" aria-current="page" class="button w-button w--current">Top Movers</a>
      <a href="#" class="button middle w-button">Large Trades</a>
      <div class="connection-info">
        <div class="status-circle"></div>
        <div>Connected</div>
      </div>
    </div>
    <div class="main-wrap">
      <GreatestGainers />
    </div>
  </div>
</template>

<script>
import GreatestGainers from "./GreatestGainers.vue";

export default {
    components: {
    GreatestGainers
}

}
</script>

<style scoped>
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
  height: 65.5px;
  padding-top: 0.5rem;
  padding-right: 0.5rem;
  padding-bottom: 0.5rem;
  padding-left: 0.5rem;
  align-items: center;
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