<script>
import { ref } from "vue";
import LocationButton from "./components/LocationButton.vue";
import SearchBar from "./components/SearchBar.vue";
import GoogleMap from "./components/GoogleMap.vue";
import LocationList from "./components/LocationList.vue";

export default {
  name: "App",
  components: { LocationButton, SearchBar, GoogleMap, LocationList },
  setup() {
    //handles user update to local coords and updates map location
    const adjustCoords = ref({});
    const handleCoordChange = (coords) => {
      adjustCoords.value = coords;
    };

    return {
      handleCoordChange,
      adjustCoords,
    };
  },
};
</script>

<template>
  <h1>Accuenergy Canada Demo</h1>
  <LocationButton @updateLocalCoords="handleCoordChange" />
  <SearchBar @updateCoords="handleCoordChange" />
  <main class="main-container">
    <GoogleMap :adjustCoords="adjustCoords" />
    <LocationList :updateList="adjustCoords" />
  </main>
</template>


<style>
#app {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.main-container {
  width: 100%;
  display: flex;
  justify-content: center;
  padding: 0 50px;
  max-width: 100vw;
}
</style>