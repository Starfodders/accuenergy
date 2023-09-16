<template>
  <h1>Accuenergy Canada</h1>
  <LocationButton />
  <SearchBar />
  <GoogleMap />
</template>

<script>
import LocationButton from "./components/LocationButton.vue";
import SearchBar from "./components/SearchBar.vue";
import GoogleMap from "./components/GoogleMap.vue";

export default {
  name: "App",
  components: { LocationButton, SearchBar, GoogleMap },
  setup() {
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