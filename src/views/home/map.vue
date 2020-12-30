<template>
  <div id="lmap"></div>
</template>

<script>
import L from "leaflet"
import "leaflet/dist/leaflet.css"
import * as chinaProvider from 'leaflet.chinatmsproviders'
import bounJson from './jeojson'
var map = null
export default {
  name: 'Map',
  data() {
    return {
      titleLayer: null,
      zoom: 5

    }
  },
  mounted() {
    this.initMap()
  },
  methods: {
    initMap() {
      var mapLayer2 = L.tileLayer.chinaProvider('Geoq.Normal.Map', {
            maxZoom: 16,
            minZoom: 3
        });
        map = L.map('lmap', {
            minZoom: 3,
            maxZoom: 16,
            center: [37, 118],
            zoom: 8,
            //  maxBounds:L.latLngBounds( L.latLng(17.6859, 64.46777),L.latLng(53.7481, 148.79883)),
            layers: [mapLayer2],
            fullscreenControl: false,
            crs: L.CRS.EPSG3857,
            zoomControl: false,
            attributionControl: false
        });
       L.control.zoom({
            position: 'bottomright'
        }).addTo(map);
        this.bondarylayer = L.geoJSON(bounJson, {
      style: {
          color: '#92969E',
          fillOpacity: 0.5,
          weight: 2,
          opacity: 0.8
      },
      pane: 'overlayPane'
  }).addTo(map);
    }
  }
}
</script>

<style lang="scss" scoped>
#lmap {
  height: calc(100vh - 95px);
  width: 100%;
      background-color: #ffffff;
}
</style>
