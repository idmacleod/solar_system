<template lang="html">
  <div id="journeyDisplay">
    <h2 id="distance">You have travelled {{ totalDistance | format_km }}.</h2>
    <destination-details
      v-for="(destination, index) in journey"
      :key="index"
      :destination="destination"
    />
  </div>
</template>

<script>
import { eventBus } from "../main.js";
import DestinationDetails from "./DestinationDetails.vue";

export default {
  name: "journey-display",
  data() {
    return {
      journey: [],
      totalDistance: 0,
    };
  },
  components: {
    "destination-details": DestinationDetails,
  },
  mounted() {
    eventBus.$on("addToJourney", (destination) => {
      this.journey.push(destination);
      this.totalDistance += destination.distance;
    });
  },
};
</script>

<style>

</style>
