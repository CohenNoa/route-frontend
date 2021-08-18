<template>
  <div id="map"></div>
</template>

<script>
import L from 'leaflet';
  export default {
    name: 'HelloWorld',
    mounted: () => {
      let map = L.map('map').setView([37.75, -122.23], 10);

      L.esri.basemapLayer('Topographic').addTo(map);
    }
   
  }
</script>
