<script>
import { defineComponent, watch, ref } from "vue";
import { GoogleMap, Marker } from "vue3-google-map";

export default defineComponent({
  components: { GoogleMap, Marker },
  props: ["adjustCoords", "currentList"],
  setup(props) {
    //default map settings of Toronto
    const center = ref({ lat: 43.6532, lng: -79.3832 });
    const zoom = ref(10);
    const markerArray = ref([])

    watch(
      () => props.adjustCoords,
      (newCoords) => {
        center.value = newCoords;
        zoom.value = 15;
      }
    );

    watch( () => props.currentList, (newItem) => {
      markerArray.value = [...newItem.value]
    }, {deep: true})

    return { center, zoom, markerArray };
  },
});
</script>

<template>
  <GoogleMap
    api-key="AIzaSyBFtORqA2gsFq4u2QP8Jgwz1AMcez4byBw"
    style="width: 70%; height: 700px; border-radius: 4px;"
    :center="center"
    :zoom="zoom"
    class = "map"
  >
    <Marker
      v-for="marker in markerArray"
      :key="`${marker.lat}-${marker.lng}`"
      :options="{ position: marker }"
    />
  </GoogleMap>
</template>

<style>
</style>