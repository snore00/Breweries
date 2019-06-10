<template lang="html">
  <div class="row map">
    <l-map
      @update:zoom="zoomUpdate"
      @update:center="centerUpdate"
      :zoom="zoom" :center="center">
      <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
      <l-marker
        :key="index"
        v-for="(brew, index) in brews"
        :lat-lng="latLng(brew.latitude, brew.longitude)">
        <l-icon
        :icon-size="brew.iconSize"
        :icon-url="icon">

        </l-icon>
      </l-marker>
    </l-map>
  </div>
  <!-- /.row map -->
</template>

<script>
  import {LMap, LTileLayer, LMarker, LIcon } from 'vue2-leaflet';
  import beer from '../assets/beer.png'
  export default {
    name: "BrewMap",
    props: {
      brews: Array
    },
    data() {
    return {
          zoom:6,
          center: L.latLng(32.868534, -111.928711),
          currentCenter: L.latLng(32.868534, -111.928711),
          currentZoom:6,
          url:'https://tile.thunderforest.com/transport/{z}/{x}/{y}.png?apikey=cd760fd465ea4bff9246f54eef56170a',
          attribution:'&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
          marker: L.latLng(47.413220, -1.219482),
          icon: beer,
          iconSize: [20,20]
        }
    },
    components: {
        LMap,
        LTileLayer,
        LMarker,
        LIcon
    },
    methods: {
      latLng: function(lat, lng) {
        return L.latLng(lat, lng);
      },

      centerUpdate: function(center) {
        this.currentCenter = center
      },
      zoomUpdate: function(zoom) {
        this.currentZoom = zoom
      }
    }
  }
</script>

<style lang="css">
 .map {
   height: 80vh;
 }
</style>
