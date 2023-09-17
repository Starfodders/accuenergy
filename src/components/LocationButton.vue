<template>
  <div class="location-container">
    <button @click="findLocation" class = "location-button">Find Your Location</button>
  </div>

</template>

<script>
import { ref } from "vue";
export default {
  name: "LocationButton",
  setup(_, {emit}) {
    let localLat = ref(null);
    let localLong = ref(null);
    let localTime = ref(null);

    const findLocation = () => {
      if (window.navigator && navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(
          (position) => {
            localLat.value = position.coords.latitude;
            localLong.value = position.coords.longitude;
            localTime.value = new Date(position.timestamp)

            //after receiving coords, emit this event and send to embedded maps
            emit('updateLocalCoords', {
              lat: localLat,
              lng: localLong,
              name: 'Your Location',
              tz: {timeZoneName: null, timeZoneID: null},
              local: localTime
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

<style>
.location-button {
  color: white;
  background-color: rgb(105, 189, 223);
  padding: 0.5rem;
  border: none;
  border-radius: 4px;
}
.location-button:hover {
  cursor: pointer;
  background-color: rgb(67, 136, 163);
  transition: all 0.3s;
}

</style>