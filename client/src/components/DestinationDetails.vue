<template>
  <div id="destination-details">
    <h2>{{ englishName }} - {{ symbol }}</h2>
    <ul>
      <li><span class="label">Mean Diameter: </span>{{ diameter }} kilometers</li>
      <li><span class="label">Gravity: </span>{{ gravity }} m/s per second</li>
      <li><span class="label">Escape Velocity: </span>{{ escape }} Meters per second</li>
      <li><span class="label">Density: </span>{{ density }} grams per cubic cm</li>
      <li v-if="moonCount"><span class="label">Number Of Moons: </span>{{ moonCount }}</li>
      <li v-if="discoveredBy"><span class="label">Discovered By: </span>{{ discoveredBy }}</li>
      <li v-if="discoveryDate"><span class="label">Discovery Date: </span>{{ discoveryDate }}</li>
      <li v-if="description"><span class="label">Description: </span>{{ description }}</li>
      <li v-if="mythology"><span class="label">Mythology: </span>{{ mythology }}</li>
    </ul>
    <img :src="destination.db.photo" />
  </div>
</template>

<script>
export default {
  name: "destination-details",
  props: ["destination"],
  data: function() {
    return {
      englishName: this.destination.api.englishName,
      density: this.destination.api.density,
      gravity: this.destination.api.gravity,
      escape: this.destination.api.escape,
      diameter: Math.floor(this.destination.api.meanRadius * 2),
      discoveredBy: this.destination.api.discoveredBy,
      discoveryDate: this.destination.api.discoveryDate,
    };
    console.log(this.moonCount);
  },
  computed: {
    description: function() {
      if (this.destination.db) {
        return this.destination.db.description;
      }
    },

    mythology: function() {
      if (this.destination.db) {
        return this.destination.db.mythology;
      }
    },
    symbol: function() {
      if (this.destination.db) {
        return this.destination.db.symbol;
      }
    },
    moonCount: function(){
      if (this.destination.api.moons) {
          return this.destination.api.moons.length;
      }
    }
  }
};
</script>

<style>
ul {
  list-style: none;
}

img {
  margin: 20px;
  max-width: 300px;
  width: auto;
  height: auto;
}
</style>
