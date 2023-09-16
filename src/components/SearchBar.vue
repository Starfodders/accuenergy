<script>
export default {
  name: "SearchBar",

  data() {
    return {
      autocomplete: null,
    };
  },

  methods: {
    handlePlaceChanged() {
      const place = this.autocomplete.getPlace();

      if (place) {
        this.$emit("updateCoords", {
          id: place.place_id,
          lat: place.geometry.location.lat(),
          lng: place.geometry.location.lng(),
          name: place.formatted_address,
        });
        // console.log(place.formatted_address);
        // console.log(place);
        // console.log(place.geometry);
        // console.log(place.geometry.location.lat(), 'lat');
        // console.log(place.geometry.location.lng(), 'lng');
      }
    },
  },

  mounted() {
    //eslint-disable-next-line
    this.autocomplete = new google.maps.places.Autocomplete(
      this.$refs.searchRef,
      {
        fields: ["place_id", "geometry", "name", "formatted_address"],
      }
    );
    this.autocomplete.addListener("place_changed", this.handlePlaceChanged);
  },
};
</script>

<template>
  <div class="search-container">
    <input
      id="autocomplete"
      placeholder="Enter a place"
      type="text"
      ref="searchRef"
    />
  </div>
</template>

<style>
.search-container {
  padding-bottom: 2rem;
}
</style>


