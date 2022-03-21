<template>
  <div class="application">
    <div class="wrapper">
      <TheSideBar />
      <div class="content">
        <router-view/>
      </div>
      <TheHotBar />
    </div>
  </div>
</template>

<script>
import TheSideBar from "./components/TheSideBar.vue"
import TheHotBar from "./components/TheHotBar.vue"

export default {
  components: {
    TheSideBar,
    TheHotBar
  },

  methods: {
    percentValueStyler(value) { return {
        'positivePct': value > 0,
        'negativePct': value < 0
      };
    },

    percentValueStylerLarge(value) { return {
        'positivePctLarge': value > 0,
        'negativePctLarge': value < 0
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
        'price-positive': value > 0,
        'price-negative': value < 0,
        'price-neutral': value = 0,
      };
    },

    currency(value) {
        return new Intl.NumberFormat('en-IN', { maximumSignificantDigits: 6 }).format(value);
    },

    numAbbr(value) {
        if (value >= 1000000000) { return (value / 1000000000).toFixed(2).replace(/\.0$/, '') + 'B'; }
        if (value >= 1000000) { return (value / 1000000).toFixed(2).replace(/\.0$/, '') + 'M'; }
        if (value >= 1000) { return (value / 1000).toFixed(2).replace(/\.0$/, '') + 'K'; }
        return value;
    },

    currencyFormatter(value) { 
        return value?.toLocaleString('en-US', { style: 'currency', currency: 'USD' });
    },
}
    
}


</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

html {
  width: 100%;
  height: 100%;
  overflow: hidden;
  position: relative;
}
</style>
