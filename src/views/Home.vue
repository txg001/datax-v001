<template>
  <div>
    <TheHighlights />
    <TheVolatilityTable />
  </div>
</template>

<script>
// @ is an alias to /src
import TheHighlights from '@/components/TheHighlights.vue'
import TheVolatilityTable from '@/components/TheVolatilityTable.vue'

export default {
  name: 'Home',
  components: {
    TheHighlights,
    TheVolatilityTable
  }
}
</script>
