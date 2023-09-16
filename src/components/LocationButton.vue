<template>
  <div class="location-container">
    <button @click="findLocation">Find Location</button>
  </div>

</template>

<script>
import { ref } from "vue";
export default {
  name: "LocationButton",
  setup(_, {emit}) {
    let localLat = ref(null);
    let localLong = ref(null);

    const findLocation = () => {
      if (window.navigator && navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(
          (position) => {
            localLat.value = position.coords.latitude;
            localLong.value = position.coords.longitude;

            //after receiving coords, emit this event and send to embedded maps
            emit('updateLocalCoords', {
              lat: localLat,
              lng: localLong
            })
            
          },
          (error) => {
            console.error("Geolocation error, ", error);
          }
        );
      } else {
        console.error("Browser does not support Geolocation");
      }
    };

    return {
      findLocation,
      localLat,
      localLong,
    };
  },
};
</script>

<style scoped>
.location-container {
  width: 15rem;
  display: flex;
  justify-content: center;
}
</style>