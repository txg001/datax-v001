<template>
  <div class="highlights_component">
      <div class="layout-1368">
        <div class="quick-statistics">
          <TopGainers />
          <TopLosers />
          <div id="w-node-e2ccbdc9-fd14-c110-6bd1-dc7efa6701cd-d98399a7" class="qs-block">
            <div class="qs-title">State of the Market</div>
            <div class="text-block-2">The total crypto market cap is <strong>$1.89T USD</strong>.<br>The market is down -7.00% over the last month and down -0.28% over the last 24 hours.</div>
          </div>
          <div id="w-node-a40b5b2b-53c7-5367-1ddf-c8201bb03b97-d98399a7" class="qs-block">
            <div class="sponsor-info"><img src="../assets/images/nexo.png" loading="lazy" alt="" class="image-2">
              <div class="sponsor-name">Nexo</div>
            </div>
            <div class="text-block-2">Unlock the Power of Your Crypto. Earn Up to 17%. Annual interest, paid out daily.<br>‍</div>
            <div class="sponser-button">
              <div>Visit Nexo.io</div>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
import TopGainers from '@/components/TopGainers.vue'
import TopLosers from '@/components/TopLosers.vue'

export default {
    components: {
      TopGainers,
      TopLosers,
    },
}
</script>

<style>

</style>