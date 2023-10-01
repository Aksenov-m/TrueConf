<script setup>
import { ref, provide } from "vue";
import ShaftContainer from "./components/ShaftContainer.vue";
import config from "./config/default.json";

const shaft = config.SHAFT;

// const elevators = {
//   floors: [1, 2],
//   isStop: [false, false, false, false, false]
// }

const elevators = ref({
  floor: 1,
  isStop: [false, false, false, false, false],
});

provide("elevators", elevators);

async function getData(i) {
  return new Promise((res) => {
    setTimeout(() => {
      res(i);
    }, 1000);
  });
}

// function cleaning(i) {
//   elevators.value.isStop[i] = true;
//   console.log(elevators.value);
// }

// function counter(f, floor) {
//   for (let i = floor; i <= f; i++) {
//     setTimeout(function () {
//       elevators.value.floors.push(i);
//       console.log("Я выполняюсь каждую секунду" + i);
//     }, 1000 * i);
//   }
// }

async function increaseFloor(f) {
  let floor = elevators.value.floor;
  // let num = Number(f);
  // if (floor) {
  //   elevators.value.isStop[f] = true;
  if (f > floor) {
    for (let i = ++floor; i <= f; i++) {
      console.log(i);
      elevators.value.floor = await getData(i);
    }
    // cleaning(f);
    console.log(elevators.value.floor);
  } else if (f < floor) {
    for (let i = --floor; i >= f; i--) {
      console.log(i);
      elevators.value.floor = await getData(i);
    }
 } else {
  return
    // console.log("Привет, пользователь!");
  }
}
// cleaning(f);
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
