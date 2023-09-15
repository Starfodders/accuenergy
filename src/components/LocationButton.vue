<template>
<div class = 'location-container'>
  <button @click = "findLocation">Find Location</button>
  </div>
</template>

<script>
import { ref } from 'vue'
export default {
  setup() {

    let localLat = ref(null)
    let localLong = ref(null)

    const findLocation = () => {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition((position) => {
          localLat.value = position.coords.latitude;
          localLong.value = position.coords.longitude;
      })
      }
      else {
        console.log('error');
      }
    }

    return {
      findLocation,
      localLat,
      localLong
    }


  }

}
</script>

<style scoped>
.location-container {
  width: 15rem;
  display: flex;
  justify-content: center;
}
</style>