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
        this.$emit('updateCoords', {
          lat: place.geometry.location.lat(),
          lng: place.geometry.location.lng()
        })
        // console.log(place);
        // console.log(place.geometry);
        // console.log(place.geometry.location.lat(), 'lat');
        // console.log(place.geometry.location.lng(), 'lng');

      }
    }
  },

  mounted() {
    //eslint-disable-next-line
    this.autocomplete = new google.maps.places.Autocomplete(
      this.$refs.searchRef,
      {
        fields: ["place_id", "geometry", "name"],
      }
    );
        this.autocomplete.addListener('place_changed', this.handlePlaceChanged);
  },
};

//place.geometry.location.lat() + lng()
</script>

<style>
.search-container {
  padding-bottom: 2rem;
}
</style>


