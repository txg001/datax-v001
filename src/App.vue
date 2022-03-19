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
}
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
