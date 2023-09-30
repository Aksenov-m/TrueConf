<script setup>
import { ref, provide } from "vue";
import ShaftContainer from "./components/ShaftContainer.vue";
import config from "./config/default.json";

const shaft = config.SHAFT;

const floors = ref([1]);
provide("floors", floors);

function increaseFloor(f) {
  // for (let i = floors.value[0]; i <= f; i += 2) {
  //   floors.value.push(i);
  // }
  console.log(f)
}
</script>

<template>
  <main class="main">
    <ShaftContainer
      v-for="item in shaft"
      :key="item"
      @handler-click="increaseFloor"
    />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.main {
  display: flex;
  flex-direction: column;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
