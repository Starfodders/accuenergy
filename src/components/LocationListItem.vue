<script>
import { ref, onMounted } from "vue";

export default {
  props: ["details", "deleteArray"],
  setup(props, {emit}) {
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

    return {
      address,
      id,
      toggleDelete,
      isChecked,
    };
  },
};
</script>

<template>
  <section class="item" ref="id">
    <div class="item-checkbox">
      <input type="checkbox" @click="toggleDelete" v-model="isChecked" />
    </div>
    <div class="item-address">
      <span>{{ address }}</span>
    </div>
  </section>
</template>

<style>
.item {
  display: flex;
  width: 100%;
  background-color: rgb(219, 219, 219);
}
.item-checkbox {
  padding: 1em 1em 1em 0.5em;
  border-right: 1px solid black;
}
.item-address {
  padding: 0 1em;
  display: flex;
  align-items: center;
}
</style>