<script setup>
import { inject } from "vue";

const props = defineProps(["floor", "active", "isUp"]);

const elevators = inject("elevators");


</script>

<template>
  <div class="information-board">
    <font-awesome-icon
      :icon="['fas', 'eject']"
      :class="[{ active: props.isUp }]"
    />
    <p class="information-board__text" :class="[{ active: props.active }]">
      {{ elevators.floor }}
    </p>
    <font-awesome-icon
      :icon="['fas', 'eject']"
      class="fa-rotate-180"
      :class="[{ active: !props.isUp }]"
    />
  </div>
</template>


<style scoped>
.information-board {
  display: flex;
  flex-direction: row;
  margin-right: 42px;
  color: grey;
}

.information-board__text {
  margin: 0 5px 10px;
  /* margin-left: 5px;
    margin-right: 5px; */
  font-size: 15px;
}

.active {
  color: red;
}
</style>