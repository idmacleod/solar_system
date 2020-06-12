<template lang="html">
  <div id="fuel-gauge">
    <GChart
      :settings="{ packages: ['gauge'] }"
      type="Gauge"
      :data="chartData"
      :options="chartOptions"
    />
  </div>
</template>

<script>
import { GChart } from 'vue-google-charts'

export default {
  name: 'fuel-gauge',
  props: ['fuel'],
  data: function () {
    return {
      chartOptions: {
        height: 150,
        max: 600,
        redFrom: 0,
        redTo: 50,
        yellowFrom: 51,
        yellowTo: 150,
        minorTicks: 10
      }
    }
  },
  computed: {
    chartData: function () {
      return [
        ['Label', 'Value'],
        ['Fuel', this.fuel]
      ];
    }
  },
  components: {
    GChart
  }
}
</script>

<style>

</style>