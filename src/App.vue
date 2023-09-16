<template>
  <h1>Accuenergy Canada</h1>
  <LocationButton @updateLocalCoords = "handleCoordChange"/>
  <SearchBar @updateCoords = "handleCoordChange"/>
  <GoogleMap :adjustCoords = "adjustCoords"/>
</template>

<script>
import {ref} from "vue";
import LocationButton from "./components/LocationButton.vue";
import SearchBar from "./components/SearchBar.vue";
import GoogleMap from "./components/GoogleMap.vue";

export default {
  name: "App",
  components: { LocationButton, SearchBar, GoogleMap },
  setup() {

    //handles user update to local coords and updates map location
    const adjustCoords = ref({})
    const handleCoordChange = (coords) => {
      adjustCoords.value = coords
    }

  return {
    handleCoordChange,
    adjustCoords
  }

  },
};
</script>

<style>
#app {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>