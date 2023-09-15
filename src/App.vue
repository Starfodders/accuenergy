<template>
  <h1>Accuenergy Canada</h1>
  <LocationButton/>
  <SearchBar/>
</template>

<script>
import LocationButton from "./components/LocationButton.vue"
import SearchBar from "./components/SearchBar.vue"

export default {
components: {LocationButton, SearchBar}
}
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