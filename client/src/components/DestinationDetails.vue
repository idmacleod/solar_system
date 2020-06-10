<template>
  <div id="destination-details">
    
    <h2>{{ englishName }} - {{ symbol }}</h2>
    
    <div id="table-div">
      <table>
        <tr><th>Mean Diameter</th><td>{{ diameter }} km</td></tr>
        <tr><th>Gravity</th><td>{{ gravity }} m/s per second</td></tr>
        <tr><th>Escape Velocity</th><td>{{ escape }} m/s</td></tr>
        <tr><th>Density</th><td>{{ density }} grams per cubic cm</td></tr>
        <tr v-if="moonCount"><th>Number Of Moons</th><td>{{ moonCount }}</td></tr>
        <tr v-if="discoveredBy"><th>Discovered By</th><td>{{ discoveredBy }}</td></tr>
        <tr v-if="discoveryDate"><th>Discovery Date</th><td>{{ discoveryDate }}</td></tr>
      </table>
    </div>
    
    <div id='details'>
      <div id="text">
        <h3>Description</h3><p>{{ description }}</p>
        <h3>Mythology</h3><p>{{ mythology }}</p>
      </div>
      <img :src="destination.db.photo" />
    </div>

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
  background: black;
  color: white;
  border: 2px solid black;
  box-shadow: 5px 5px 10px #00000066;
}

h2, h3 {
  font-family: 'Nixie One';
  text-align: center;
  margin: 0;
  padding: 10px;
}

#table-div {
  display: flex;
  justify-content: center;
  background: white;
}

#table-div table {
  border: 2px solid black;
  border-collapse: collapse;
  margin: 10px;
  box-shadow: 5px 5px 10px #00000066;
}

th {
  text-align: right;
  padding: 5px;
  background: black;
  color: white;
}

td {
  padding: 5px;
  background: white;
  color: black;
}

#details {
  display: flex;
  align-items: center;
}

#text {
  margin: 10px;
}

img {
  width: 40%;
  height: 40%;
  margin: 10px;
}
</style>
