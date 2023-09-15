<template>
  <h1>Accuenergy Canada</h1>
  <LocationButton/>
</template>

<script>
import LocationButton from "./components/LocationButton.vue"
export default {
components: {LocationButton}
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