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

</style>