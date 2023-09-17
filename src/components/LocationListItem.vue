<script>
import { ref, onMounted } from "vue";

export default {
  props: ["details", "deleteArray"],
  setup(props, { emit }) {
    const id = ref(null);
    const address = ref(null);
    const isChecked = ref(false);

    onMounted(() => {
      address.value = props.details.name;
      id.value = props.details.id;
    });

    const toggleDelete = () => {
      if (!isChecked.value) {
        if (!props.deleteArray.includes(props.details.id)) {
          emit("addToArray", props.details.id);
        }
      } else {
        const index = props.deleteArray.indexOf(props.details.id);
        if (index !== -1) {
          emit("removeFromArray", props.details.id);
        }
      }
    };

    const handleSwitch = () => {
      emit("switchLocations", props.details);
    };

    return {
      address,
      id,
      toggleDelete,
      isChecked,
      handleSwitch,
    };
  },
};
</script>

<template>
  <section :class="!isChecked ? 'item'  : 'item-flagged'" ref="id">
    <div class="item-checkbox">
      <input type="checkbox" @click="toggleDelete" v-model="isChecked" />
    </div>
    <div class="item-address" @click="handleSwitch">
      <span>{{ address }}</span>
    </div>
  </section>
</template>

<style>
.item {
  display: flex;
  width: 100%;
  background-color: rgb(248, 248, 248);
  border-bottom: 1px solid black;
}
.item-flagged {
  display: flex;
  width: 100%;
  background-color: rgb(255, 219, 219);
  border-bottom: 1px solid black; 
}
.item:hover {
    background-color: rgb(213, 213, 213);
    cursor: pointer;
    transition: all 0.3;
}
.item-checkbox {
  padding: 1em 0.2em;
  width: 10%;
  border-right: 1px solid black;
  display: flex;
  justify-content: center;
}
.item-address {
  padding: 0 1em;
  display: flex;
  width: 90%;
  align-items: center;
}
</style>


IF YOU'RE READING THIS, NEED TO TIE THE MAP MARKERS NOT TO JUST ADJUSTCOORDS BUT TO THE LOCAITONSARRAY 
SO THAT WHEN THEY'RE DELETED, THEY CAN ALSO BE REMOVED FROM THE MAP. CAN ALSO ONLY SHOW 10 AT A TIME