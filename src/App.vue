<template>
  <div id="app">
    <l-map     
      style="height: 500px; width: 100%"
      :zoom="zoom"
      :center="center"
    >
      <l-tile-layer :url="url"></l-tile-layer>
      <l-marker :icon="icon" :lat-lng="markerLatLng" >
        <l-popup>Hello!</l-popup>
      </l-marker>
      <l-geo-json :geojson="geojson"></l-geo-json>
    </l-map>
  </div>
</template>

<script>
import {LMap, LTileLayer, LMarker, LPopup, LGeoJson} from 'vue2-leaflet'
import 'leaflet/dist/leaflet.css'
import L from 'leaflet'
import axios from 'axios'

export default {
  name: 'app',
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LPopup,
    LGeoJson
  },
  data: function() {
    const myMarkerIcon = L.icon({
      iconUrl: require('leaflet/dist/images/marker-icon.png'),
      shadowUrl: require('leaflet/dist/images/marker-shadow.png'),
      iconRetinaUrl: require('leaflet/dist/images/marker-icon-2x.png')
    });
    return {
      zoom: 8,
      center: [47.413220, -1.219482],
      markerLatLng: [47.413220, -1.219482],
      url: 'http://{s}.tile.osm.org/{z}/{x}/{y}.png',
      icon: myMarkerIcon,
      geojson: null
    }
  },
  created() {
    axios.get('https://rawgit.com/gregoiredavid/france-geojson/master/regions/pays-de-la-loire/communes-pays-de-la-loire.geojson').then((response) => {
      this.geojson = response.data;
    })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
