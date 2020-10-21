<template>
  <div id="container">
    <div class="map-container">
      <LMap id="map" :center="center" :minZoom="minZoom" :maxZoom="maxZoom" :bounds="bounds" :max-bounds="maxBounds">
        <LTileLayer :url="url"/>
      </LMap>
    </div>
    <LocationCard :connection="'Millenium'"/>
  </div>
  
</template>

<script>
import L from 'leaflet';
import { latLngBounds } from "leaflet";
import { LMap, LTileLayer } from 'vue2-leaflet';
import mapboxgl from 'mapbox-gl'

import 'mapbox-gl-leaflet'
import 'mapbox-gl/dist/mapbox-gl.css'
import 'leaflet/dist/leaflet.css'

import LocationCard from '../LocationCard/LocationCard'

window.mapboxgl = mapboxgl

export default {
  name: 'MapboxMap',
  props: {},
  components: {
    LMap,
    LTileLayer,
    LocationCard
  },
  data() {
    return {
      center: L.latLng(51.5123437, -0.0955912),
      minZoom: 14,
      maxZoom: 15,
      bounds: latLngBounds([[51.5123000,  -0.0846589],[51.50000,  -0.1146131]]),
      maxBounds: latLngBounds([[51.5123000,  -0.0846589],[51.50000,  -0.1146131]]),
      url:`http://api.mapbox.com/styles/v1/bnulens/ckggny7ao00u219o6zyntnmja/tiles/256/{z}/{x}/{y}@2x?access_token=pk.eyJ1IjoiYm51bGVucyIsImEiOiJja2dnbzRwcTcwMzc5MnFsajdqMGlwM2h3In0.tk7oltSZoRA3zTEcrAZmIA`,
    }
  }
}
</script>

<style lang="scss" scoped>
  @import '@/assets/scss/_vars.scss';

  #container {
    .map-container {
      position: absolute;
      height: 100%;
      width: 100%;

      @media screen and (min-width: 768px) {
        z-index: 0;
        width: 70%;
        height: 100vh;
      }
    }
  }
</style>