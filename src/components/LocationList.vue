<script>
import { watch, ref, computed } from "vue";
import LocationListItem from "./LocationListItem.vue";

export default {
  props: ["updateList"],
  components: { LocationListItem },
  setup(props, { emit }) {
    //when there is a new location, push into locations array which then updates the LocationListItem
    const locationsArray = ref([]);
    //contains the items to be removed from list
    const deleteArray = ref([]);
    //code to handle table display and pagination
    const currentPage = ref(1);
    const itemsPerPage = 3;

    const totalPages = computed(() => {
      return Math.max(1, Math.ceil(locationsArray.value.length / itemsPerPage));
    });

    const itemsToDisplay = computed(() => {
      const start = (currentPage.value - 1) * itemsPerPage;
      const end = start + itemsPerPage;
      return locationsArray.value.slice(start, end);
    });

    const handleNextListPage = () => {
      if (currentPage.value <= totalPages.value) {
        currentPage.value++;
      }
    };

    const handlePrevListPage = () => {
      if (currentPage.value > 1) {
        currentPage.value--;
      }
    };

    watch(
      () => props.updateList,
      (newValue) => {
        //first check if it exists to prevent duplication when switching
        if (
          !locationsArray.value.some((location) => location.id === newValue.id)
        ) {
          locationsArray.value.push(newValue);
          emit("retrieveList", locationsArray);
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
      emit("retrieveList", locationsArray);
    };

    const handleSwitch = (details) => {
      emit("switchLocations", details);
    };

    // ...

    return {
      locationsArray,
      itemsToDisplay,
      deleteArray,
      handleAdd,
      handleRemove,
      deleteSelected,
      handleSwitch,
      currentPage,
      totalPages,
      handleNextListPage,
      handlePrevListPage,
    };
  },
};
</script>

<template>
  <div class="list-container">
    <div class = "list-topwrapper">
    <div class="list-container-top">
      <button
        @click="deleteSelected"
        :class="
          deleteArray.length > 0 ? 'delete-button' : 'delete-button-disabled'
        "
      >
        Remove Selected
      </button>
    </div>
    <div class="list-container-main">
      <LocationListItem
        v-for="location in itemsToDisplay"
        :key="location.id"
        :details="location"
        :deleteArray="deleteArray"
        @addToArray="handleAdd"
        @removeFromArray="handleRemove"
        @switchLocations="handleSwitch"
      />
    </div>
    </div>
    <div class="list-pagination">
      <button @click="handlePrevListPage" :disabled = "currentPage <= 1">
        <span class="material-symbols-outlined"> arrow_back </span>Prev
      </button>
      <span>Page {{ currentPage }} of {{ totalPages }}</span>
      <button @click="handleNextListPage" :disabled="currentPage >= totalPages">
        <span class="material-symbols-outlined"> arrow_forward </span>Next
      </button>
    </div>
  </div>
</template>

<style scoped>
.list-container {
  width: 30%;
  max-width: 25em;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 0 1em;
}
.list-container-top {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0.5rem 0;
  background-color: rgb(243, 243, 243);
}
.list-container-main {
  width: 100%;
  display: flex;
  flex-direction: column;
  border: 1px solid black;
  border-bottom: none;
  border-radius: 4px;
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
.list-pagination {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-top: 0.3rem;
}
</style>