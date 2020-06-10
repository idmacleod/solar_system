<template>
  <nav>

    <table>
      <tr><th>Currently Orbiting</th><td>{{ currentLocationName }}</td></tr>
      <tr><th>Distance Travelled</th><td>{{ distanceTravelled | format_km }}</td></tr>
      <tr>
        <th>Set Destination</th>
        <td>
          <select id="select" v-model="selectedDestinationName">
            <option value="" disabled>Please Select</option>
              <option
                v-for="(destination, index) in filterPlanets"
                :key="index"
                :value="destination.englishName"
              >{{ destination.englishName }}</option>
            </select>
        </td>
      </tr>
    </table>
    
    <table>
      <tr><th>Distance To Destination</th><td>{{ distanceToDestination | format_km }}</td></tr>
      <tr><th>Fuel Required</th><td>{{ fuelRequired }}</td></tr>
      <tr><th>Engines</th><td><button v-on:click="engageEngines">Engage</button></td></tr>
    </table>

    <fuel-gauge :fuel="fuel" id="gauge"></fuel-gauge>

  </nav>
</template>

<script>
import { eventBus } from "@/main.js";
import FuelGauge from "@/components/FuelGauge.vue";

export default {
  name: "journey-form",
  props: ["all_destinations", "details"],
  data: function() {
    return {
      currentLocationName: "Earth",
      selectedDestinationName: "",
      distanceTravelled: 0,
      fuel: 600
    };
  },
  computed: {
    currentLocation: function() {
      return this.all_destinations.find(
        destination => destination.englishName === this.currentLocationName
      );
    },
    currentLocationDetails: function() {
      return this.details.find(
        destination => destination.api_id === this.currentLocation.id
      );
    },
    selectedDestination: function() {
      if (this.selectedDestinationName) {
        return this.all_destinations.find(
          destination => destination.englishName === this.selectedDestinationName
        );
      }
    },
    selectedDestinationDetails: function() {
      if (this.selectedDestination) {
        return this.details.find(
          destination => destination.api_id === this.selectedDestination.id
        );
      }
    },
    filterPlanets: function() {
      return this.all_destinations.filter(
        destination => destination.englishName != this.currentLocationName && this.hasDetails(destination)
      );
    },
    distanceToDestination: function() {
      return this.selectedDestination ? this.currentLocationDetails.distance_to[this.selectedDestination.id] : 0;
    },
    fuelRequired: function() {
      return this.selectedDestination ? Math.floor(this.distanceToDestination / 40000000) : 0;
    }
  },
  methods: {
    engageEngines: function() {
      if (this.fuelRequired <= this.fuel) {
        eventBus.$emit("addToJourney", {
          api: this.selectedDestination,
          db: this.selectedDestinationDetails,
          distance: this.distanceToDestination,
        });
        this.fuel -= this.fuelRequired;
        this.distanceTravelled += this.distanceToDestination;
        this.currentLocationName = this.selectedDestinationName;
      }
      this.selectedDestinationName = "";
    },
    hasDetails: function(destination) {
      return this.details.some(details => details.api_id === destination.id);
    },
  },
  components: {
    "fuel-gauge": FuelGauge,
  },
};
</script>

<style>
nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

nav table {
  border: 2px solid black;
  padding: 5px;
}

nav th {
  text-align: right;
  background: black;
  color: white;
  padding: 5px;
}

nav td {
  padding: 5px;
}

select, button {
  font-family: inherit;
}
</style>