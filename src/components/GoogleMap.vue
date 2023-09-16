<script>
import { defineComponent, watch, ref } from "vue";
import { GoogleMap, Marker } from "vue3-google-map";

export default defineComponent({
  components: { GoogleMap, Marker },
  props: ["adjustCoords"],
  setup(props) {
    //default map settings of Toronto
    const center = ref({ lat: 43.6532, lng: -79.3832 });
    const zoom = ref(10);

    watch(
      () => props.adjustCoords,
      (newCoords) => {
        center.value = newCoords;
        zoom.value = 15;
      }
    );

    return { center, zoom };
  },
});
</script>

<template>
  <GoogleMap
    api-key="AIzaSyBFtORqA2gsFq4u2QP8Jgwz1AMcez4byBw"
    style="width: 70%; height: 700px"
    :center="center"
    :zoom="zoom"
  >
    <Marker :options="{ position: center }" />
  </GoogleMap>
</template>

<style>
</style>