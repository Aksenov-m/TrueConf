<script setup>
import {
  provide,
  onBeforeMount,
  reactive,
} from "vue";
import ShaftContainer from "./components/ShaftContainer.vue";
import config from "./config/default.json";

const shaft = config.SHAFT;

const elevators = reactive({
  floor: 1,
});

onBeforeMount(() => {
  if (localStorage.floor) {
    elevators.floor = localStorage.floor;
  }
});

provide("elevators", elevators);

async function getData(i) {
  return new Promise((res) => {
    setTimeout(() => {
      res(i);
    }, 1000);
  });
}

async function assignments(i) {
  elevators.floor = await getData(i);
}


async function increaseFloor(f) {
  let floor = elevators.floor;
  if (f > floor) {
    for (let i = ++floor; i <= f; i++) {
      await assignments(i);
    }
  } else if (f < floor) {
    for (let i = --floor; i >= f; i--) {
      await assignments(i);
    }
  } else {
    return;
  }
  localStorage.setItem("floor", elevators.floor);
}

async function increase(f) {
  await increaseFloor(f);
}

</script>

<template>
  <main class="main">
    <ShaftContainer
      v-for="item in shaft"
      :key="item"
      @handler-click="increase"
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
