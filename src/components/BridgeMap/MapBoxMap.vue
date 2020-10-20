<template>
  <div id="container">
    <div class="map-container">
      <!-- <LMap id="map" :center="center" :minZoom="minZoom" :maxZoom="maxZoom" :bounds="bounds" :max-bounds="maxBounds"> -->
      <LMap id="map" :center="center" :minZoom="minZoom" :maxZoom="maxZoom">
        <LTileLayer :url="url"/>
      </LMap>
    </div>
    <LocationCard :connection="'Millenium'"/>
  </div>
  
</template>

<script>
import L from 'leaflet';
// import { latLngBounds } from "leaflet";
import { LMap, LTileLayer } from 'vue2-leaflet';
import mapboxgl from 'mapbox-gl'

import 'mapbox-gl-leaflet'
import 'mapbox-gl/dist/mapbox-gl.css'
import 'leaflet/dist/leaflet.css'

import LocationCard from './LocationCard'

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
      center: L.latLng(51.5101559, -0.0979333),
      minZoom: 14,
      maxZoom: 15,
      // bounds: latLngBounds([[51.5029024,  -0.1146589],[51.5052242,  -0.1146131]]),
      // maxBounds: latLngBounds([[51.5017936,  -0.1202588],[51.5052242,  -0.1146131]]),
      url:`http://api.mapbox.com/styles/v1/bnulens/ckggny7ao00u219o6zyntnmja/tiles/256/{z}/{x}/{y}@2x?access_token=pk.eyJ1IjoiYm51bGVucyIsImEiOiJja2dnbzRwcTcwMzc5MnFsajdqMGlwM2h3In0.tk7oltSZoRA3zTEcrAZmIA`,
    }
  }
}
</script>

<style lang="scss" scoped>
  @import '@/assets/scss/_vars.scss';

  #container {
    .map-container {
      display: block;
      #map {
        position: absolute;
        top: 0;
        height: 100%;
        overflow: hidden;
      }
      @media screen and (max-width: 768px) {
        z-index: 0;
        width: 100vw;
      }
    }
  }
</style>