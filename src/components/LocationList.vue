<script>
import { watch, ref } from "vue";
import LocationListItem from "./LocationListItem.vue";

export default {
  props: ["updateList"],
  components: { LocationListItem },
  setup(props) {
    //when there is a new location, push into locations array which then updates the LocationListItem
    const locationsArray = ref([]);
    const deleteArray = ref([]);

    watch(
      () => props.updateList,
      () => {
        locationsArray.value.push(props.updateList);
      }
    );

    const handleAdd = (id) => {
      deleteArray.value.push(id);
    };
    const handleRemove = (id) => {
      const index = deleteArray.value.indexOf(id);
      if (index !== -1) {
        deleteArray.value.splice(index, 1);
      }
    };

    const deleteSelected = () => {
      locationsArray.value = locationsArray.value.filter(
        (location) => !deleteArray.value.includes(location.id)
      );
      deleteArray.value = [];
    };

    return {
      locationsArray,
      deleteArray,
      handleAdd,
      handleRemove,
      deleteSelected,
    };
  },
};
</script>

<template>
  <div class="list-container">
    <div class="list-container-top">
      <button @click="deleteSelected">Remove Selected</button>
    </div>
    <div class="list-container-main">
      <LocationListItem
        v-for="location in locationsArray"
        :key="location.id"
        :details="location"
        :deleteArray="deleteArray"
        @addToArray="handleAdd"
        @removeFromArray="handleRemove"
      />
    </div>
  </div>
</template>

<style scoped>
.list-container {
  width: 30%;
  max-width: 25em;
  display: flex;
  flex-direction: column;
  padding: 0 1em;
}
.list-container-top {
  width: 100%;
  background-color: red;
}
.list-container-main {
  width: 100%;
  display: flex;
  flex-direction: column;
}
</style>