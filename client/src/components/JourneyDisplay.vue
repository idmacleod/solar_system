<template lang="html">
  <div id="journey-display">
    <journey-symbols />
    <div id="cards">
      <destination-details
        v-for="(destination, index) in journey"
        :key="index"
        :destination="destination"
      />
    </div>
  </div>
</template>

<script>
import { eventBus } from "../main.js";
import JourneySymbols from "./JourneySymbols.vue";
import DestinationDetails from "./DestinationDetails.vue";

export default {
  name: "journey-display",
  data() {
    return {
      journey: []
    };
  },
  computed: {
    symbols: function () {
      return this.journey.map(destination => destination.db.symbol);
    }
  },
  mounted() {
    eventBus.$on("addToJourney", (destination) => {
      this.journey.push(destination);
    });
  },
  components: {
    "journey-symbols": JourneySymbols,
    "destination-details": DestinationDetails
  }
};
</script>

<style>
#cards {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}
</style>
