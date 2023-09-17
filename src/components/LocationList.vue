<script>
import { watch, ref } from "vue";
import LocationListItem from "./LocationListItem.vue";

export default {
  props: ["updateList"],
  components: { LocationListItem },
  setup(props, { emit }) {
    //when there is a new location, push into locations array which then updates the LocationListItem
    const locationsArray = ref([]);
    const deleteArray = ref([]);

    watch(
      () => props.updateList,
      (newValue) => {
        //first check if it exists to prevent duplication when switching
        if (!locationsArray.value.some((location) => location.id === newValue.id)) {
          locationsArray.value.push(newValue);
          emit('retrieveList', locationsArray);
        }
      }
    );

    //adds if checked
    const handleAdd = (id) => {
      deleteArray.value.push(id);
    };

    //removed if unchecked
    const handleRemove = (id) => {
      const index = deleteArray.value.indexOf(id);
      if (index !== -1) {
        deleteArray.value.splice(index, 1);
      }
    };

    //deletes selected entries
    const deleteSelected = () => {
      locationsArray.value = locationsArray.value.filter(
        (location) => !deleteArray.value.includes(location.id)
      );
      deleteArray.value = [];
      emit('retrieveList', locationsArray)
    };

    const handleSwitch = (details) => {
      emit("switchLocations", details);
    };

    return {
      locationsArray,
      deleteArray,
      handleAdd,
      handleRemove,
      deleteSelected,
      handleSwitch,
    };
  },
};
</script>

<template>
  <div class="list-container">
    <div class="list-container-top">
      <button @click="deleteSelected" :class="deleteArray.length > 0 ? 'delete-button' : 'delete-button-disabled'">Remove Selected</button>
    </div>
    <div class="list-container-main">
      <LocationListItem
        v-for="location in locationsArray"
        :key="location.id"
        :details="location"
        :deleteArray="deleteArray"
        @addToArray="handleAdd"
        @removeFromArray="handleRemove"
        @switchLocations="handleSwitch"
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
  display: flex;
  justify-content: center;
  padding-bottom: 1rem;
}
.list-container-main {
  width: 100%;
  display: flex;
  flex-direction: column;
}
.delete-button {
  color: white;
  background-color: rgb(105, 189, 223);
  padding: 0.5rem;
  border: none;
  border-radius: 4px;
}
.delete-button-disabled {
color: white;
  background-color: rgb(105, 189, 223);
  padding: 0.5rem;
  border: none;
  border-radius: 4px;
  opacity: 0.5;
    pointer-events: none;
}
</style>