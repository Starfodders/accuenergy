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
      }
    },
    clearField() {
      this.$refs.searchRef.value = ''
    },
    selectFirst(e) {
      const dropdown = document.querySelector('.pac-container');
      //handles lack of dropdown option
      if (!dropdown) {
        return
      }
      //this addresses if user already has the first suggestion picked, won't erroneously pick the second
      const firstSuggestion = document.querySelector('.pac-item');
      if (!firstSuggestion || firstSuggestion.classList.contains('pac-item-selected')) {
      return;
      }
      const downPress = new KeyboardEvent("keydown", {
        keyCode: 40,
        which: 40
      });
      e.target.dispatchEvent(downPress);
      this.$refs.searchRef.value = ''
    }
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
      @click = "clearField"
      @keydown.enter = "selectFirst"
    />
  </div>
</template>

<style>
/* .search-container {
} */
#autocomplete {
  min-width: 20rem;
  padding: 0.4rem 0.5rem;
  border: 2px solid rgb(105, 189, 223);
  color: rgb(62, 62, 62);
  border-radius: 4px;
}
</style>


