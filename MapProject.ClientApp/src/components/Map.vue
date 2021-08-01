<template>
  <l-map style="height:50vh">
    <l-geo-json :geojson="geojson" :options="geojsonOptions" />
  </l-map>
</template>

<script lang="ts">
  import 'leaflet/dist/leaflet.css'

  // https://github.com/vue-leaflet/vue-leaflet
  import { LMap, LGeoJson } from '@vue-leaflet/vue-leaflet'

  export default {
    components: {
      LMap,
      LGeoJson,
    },

    data(): any {
      return {

        geojson: {
          type: "FeatureCollection",
          features: [
            // ...
          ],
        },

        geojsonOptions: {
          // Options that don't rely on Leaflet methods.
        },

      }
    },

    async beforeMount() {
      // HERE is where to load Leaflet components!
      const { circleMarker } = await import('leaflet/dist/leaflet-src.esm');

      // And now the Leaflet circleMarker function can be used by the options:
      this.geojsonOptions.pointToLayer = (feature, latLng) =>
        circleMarker(latLng, { radius: 8 });
      this.mapIsReady = true;
    },
  }
</script>

<style lang="scss" scoped>

</style>
