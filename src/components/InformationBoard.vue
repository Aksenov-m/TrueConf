<script setup>
import { watch, inject } from "vue";

const props = defineProps(["floor", "active"]);

const elevators = inject("elevators");

// const isCall = computed(() => {
//   return elevators.value.floor === props.floor ? true : false
// })

</script>

<template>
  <div class="information-board">
    <font-awesome-icon :icon="['fas', 'eject']" />
    <p class="information-board__text" :class="[{ active: props.active }]">
      {{ elevators.floor }}
    </p>
    <font-awesome-icon :icon="['fas', 'eject']" class="fa-rotate-180" />
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