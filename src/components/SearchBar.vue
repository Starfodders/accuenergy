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
      autocomplete: null
    };
  },

  mounted() {
    //eslint-disable-next-line
    this.autocomplete = new google.maps.places.Autocomplete(this.$refs.searchRef, {
      fields: ["place_id", "geometry", "name", "address"]
    });
  }
};
</script>

<style>
.search-container {
  padding-bottom: 2rem;
}
</style>
