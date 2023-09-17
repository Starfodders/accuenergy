<script>
import { ref, watch } from "vue";
export default {
  props: ["location"],
  setup(props) {
    const address = ref(null);
    const localTime = ref(null);
    const timeZoneID = ref(null);
    const timeZoneName = ref(null);

    watch(
      () => props.location,
      () => {
        address.value = props.location.name;
        timeZoneID.value = props.location.tz.timeZoneId;
        timeZoneName.value = props.location.tz.timeZoneName;

        const localTimestamp =
          Date.now() / 1000 +
          props.location.tz.rawOffset +
          props.location.tz.dstOffset;
        const formattedDate = new Date(localTimestamp * 1000);
        localTime.value = formattedDate.toLocaleTimeString();
      }
    );

    return {
      address,
      localTime,
      timeZoneID,
      timeZoneName
    };
  },
};
</script>

<template>
  <div class="recent-box" v-if="address">
    <p>{{ address }}</p>
    <p>Local Time: {{ localTime }}</p>
    <p>Timezone: {{ timeZoneName }} : {{timeZoneID}}</p>
  </div>
</template>

<style>
.recent-box {
  position: absolute;
  top: 1%;
  left: 1%;
  width: 30%;
  min-width: 100px;
  min-height: 50px;
  background-color: rgba(243, 243, 243, 0.7);
  border: 1px solid black;
  border-radius: 4px;
  padding: 0.5rem;
  font-size: 0.7rem;
}
</style>