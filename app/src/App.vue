<template>
  <v-container>
    <v-row no-gutters justify="space-around">
      <v-col md="4" class="d-flex justify-center align-center">
          <v-btn
      class="mx-2"
      fab
      dark
      color="primary"
      @click="changeColor('red')"
    >
      נ.ס
    </v-btn>
      </v-col>
      <v-col md="4" class="d-flex justify-center align-center">
          <v-btn
      class="mx-2"
      fab
      dark
      color="primary"
      @click="changeColor('blue')"
    >
      <v-icon>
        mdi-plus
      </v-icon>
    </v-btn>
      </v-col>
      <v-col md="4" class="d-flex justify-center align-center">
          <v-btn
      class="mx-2"
      fab
      dark
      color="primary"
      @click="changeColor('green')"
    >
      נ.ה
    </v-btn>
      </v-col>
      
      
    </v-row>
    <div id="map"></div>
  </v-container>
</template>

<script>
import * as L from 'leaflet';
import * as esri from 'esri-leaflet';

export default {
  name: 'App',
  data() {
    return {
      color: '',
      steps: new Array()
    }
  },
  methods: {
    changeColor: function(newColor) {
      this.color = newColor;
    }
  },
  mounted: function() {
      const outerThis = this;
      let map = L.map('map').setView([30.655612, 34.790354], 10);
      esri.basemapLayer('Topographic').addTo(map);
      map.on('click', function(e) {
          const latlng = e.latlng;
          const color = outerThis.color;
          if (color) {
            switch(color) {
              case "green":
                outerThis.steps.unshift(latlng);
                break;
              case "blue":
                outerThis.steps.splice(2, 0, latlng);
                break;
              case "red":
                outerThis.steps.push(latlng);
                break;
            }
            const icon = 
              new L.Icon({
                iconUrl: `https://raw.githubusercontent.com/pointhi/leaflet-color-markers/master/img/marker-icon-2x-${color}.png`,
                shadowUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/0.7.7/images/marker-shadow.png',
                iconSize: [25, 41],
                iconAnchor: [12, 41],
                popupAnchor: [1, -34],
                shadowSize: [41, 41]
              });
            L.marker(latlng, {icon: icon}).addTo(map);
            console.log(outerThis.steps)
          }
      });
  }
};
</script>
