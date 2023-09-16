<script>
import { ref, onMounted } from "vue";

export default {
  props: ["details"],
  setup(props) {
    const address = ref(null);
    onMounted(() => {
      console.log("Props passed to child:", props.details);
      address.value = props.details.name;
    });

    return {
      address,
    };
  },
};
</script>

<template>
  <div class="item-checkbox">
    <input type="checkbox" />
  </div>
  <div class="item-address">
    <span>{{ address }}</span>
  </div>
</template>

<style>
</style>