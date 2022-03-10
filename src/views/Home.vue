<template>
  <div>
    <TheHighlights />
    <VolatilityMarketCapWidget />
  </div>
</template>

<script>
// @ is an alias to /src
import TheHighlights from '@/components/TheHighlights.vue'
import VolatilityMarketCapWidget from '@/components/VolatilityMarketCapWidget.vue'

export default {
  name: 'ByVolatilityTable',
  components: {
    TheHighlights,
    VolatilityMarketCapWidget
  }
}
</script>
