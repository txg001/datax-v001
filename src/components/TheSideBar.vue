<template>
  <div class="sidebar">
        <div class="div-block-4"><img src="images/DataX-Light.svg" loading="lazy" alt="" class="image-5">
          <div class="text-block-5">v 0.01a</div>
        </div>
        <div class="link-block">
          <div class="sidebar-title">Cryptocurrencies</div>
          <router-link :to="{ path: '/' }" class="link">Market Cap Rank</router-link>
        </div>
        <div class="link-block">
          <div class="sidebar-title">Misc.</div>
          <router-link :to="{ path: '/about' }" class="link">Sandbox - About</router-link>
        </div>
      </div>
</template>

<script>
export default {

}
</script>

<style>

</style>