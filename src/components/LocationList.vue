<script>
import { watch, ref } from "vue";
import LocationListItem from "./LocationListItem.vue"

export default {
  props: ['updateList'],
  components: {LocationListItem},
  setup(props) {
    
    //when there is a new location, push into locations array which then updates the LocationListItem
    const locationsArray = ref([])


    watch(() => props.updateList, () => {
       locationsArray.value.push(props.updateList)

    })

    return {
        locationsArray
    };
  },
};
</script>

<template>
  <div class="list-container">
    <div class="list-container-top">
        <button>Remove Selected</button>
    </div>
    <div class="list-container-main">
        <LocationListItem v-for = "location in locationsArray" :key = "location.id" :details = "location"/>
    </div>
  </div>
</template>

<style scoped>
.list-container {
  width: 30%;
  max-width: 25em;
  display: flex;
  flex-direction: column;
}
.list-container-top {
    width: 100%;
    background-color: red;
}
.list-container-main {
    width: 100%;
    display: flex;
}
</style>