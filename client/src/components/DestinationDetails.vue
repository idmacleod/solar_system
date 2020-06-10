<template>
  <div id="destination-details">
    
    <h2>{{ englishName }} - {{ symbol }}</h2>
    
    <div id="card-top">
      <table>
        <tr><th>Mean Diameter</th><td>{{ diameter }} km</td></tr>
        <tr><th>Gravity</th><td>{{ gravity }} m/s per second</td></tr>
        <tr><th>Escape Velocity</th><td>{{ escape }} m/s</td></tr>
        <tr><th>Density</th><td>{{ density }} grams per cubic cm</td></tr>
        <tr v-if="moonCount"><th>Number Of Moons</th><td>{{ moonCount }}</td></tr>
        <tr v-if="discoveredBy"><th>Discovered By</th><td>{{ discoveredBy }}</td></tr>
        <tr v-if="discoveryDate"><th>Discovery Date</th><td>{{ discoveryDate }}</td></tr>
      </table>
      <img :src="destination.db.photo" />
    </div>
    
    <div v-if="description" id="description"><h3>Description</h3><p>{{ description }}</p></div>
    
    <div v-if="mythology" id="mythology"><h3>Mythology</h3><p>{{ mythology }}</p></div>

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
#destination-details {
    border: 2px solid black;
    margin: 10px;
}

h2 {
  font-family: 'Nixie One';
  margin: 0 0 0 0;
  padding: 10px;
  text-align: justify;
}

#card-top {
  display: flex;
  justify-content: space-around;
  align-items: center;
  background: black;
  color: white;
}

table {
  border: 2px solid white;
  border-collapse: collapse;
}

th {
  text-align: right;
  background: white;
  color: black;
  padding: 5px;
}

td {
  padding: 5px;
}

img {
  max-width: 200px;
  margin: 10px;
}

#description, #mythology {
  padding: 10px;
}

h3 {
  margin: 0;
}

#mythology {
  background: black;
  color: white;
}
</style>
