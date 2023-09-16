<template>
  <div class="location-container">
    <button @click="findLocation">Find Location</button>
  </div>
  {{localLat}}
  {{localLong}}

</template>

<script>
import { ref } from "vue";
export default {
  name: "LocationButton",
  setup() {
    let localLat = ref(null);
    let localLong = ref(null);

    const findLocation = () => {
      if (window.navigator && navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(
          (position) => {
            localLat.value = position.coords.latitude;
            localLong.value = position.coords.longitude;
            
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