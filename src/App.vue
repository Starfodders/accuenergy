<script>
import { ref } from "vue";
import LocationButton from "./components/LocationButton.vue";
import SearchBar from "./components/SearchBar.vue";
import GoogleMap from "./components/GoogleMap.vue";
import LocationList from "./components/LocationList.vue";
import RecentPlace from "./components/RecentPlace.vue";

export default {
  name: "App",
  components: {
    LocationButton,
    SearchBar,
    GoogleMap,
    LocationList,
    RecentPlace,
  },
  setup() {
    //handles user update to local coords and updates map location
    const adjustCoords = ref({});
    const handleCoordChange = (coords) => {
      adjustCoords.value = coords;
    };

    const currentList = ref([]);
    const forwardList = (data) => {
      currentList.value = data;
    };

    return {
      handleCoordChange,
      adjustCoords,
      forwardList,
      currentList,
    };
  },
};
</script>

<template>
  <h1 class="title">Accuenergy Canada Demo</h1>
  <p>Submitted by Michael Deng</p>
  <main class="main-container">
    <GoogleMap :adjustCoords="adjustCoords" :currentList="currentList" />
    <LocationList
      :updateList="adjustCoords"
      @switchLocations="handleCoordChange"
      @retrieveList="forwardList"
    />
  </main>
  <div class="main-bottom">
    <LocationButton @updateLocalCoords="handleCoordChange" />
    <SearchBar @updateCoords="handleCoordChange" />
  </div>
  <RecentPlace :location="adjustCoords" />
</template>


<style>
#app {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  font-family: "Roboto", sans-serif;
}
.title {
  margin-bottom: 0;
}
.main-container {
  width: 100%;
  display: flex;
  justify-content: center;
  padding: 0 50px;
  max-width: 100vw;
}
.main-bottom {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1rem;
  padding: 2rem 0;
}
</style>