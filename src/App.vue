<script setup>
import { ref, provide, watch, nextTick } from "vue";
import ShaftContainer from "./components/ShaftContainer.vue";
import config from "./config/default.json";

const shaft = config.SHAFT;

// const elevators = {
//   floors: [1, 2],
//   isStop: [false, false, false, false, false]
// }

const elevators = ref({
  floor: 1
});
let floor = elevators.value.floor;
// const count = ref(0)
// watch(count, (count) => {
//   console.log(`count is: ${count}`)
// })

provide("elevators", elevators);

async function getData(i) {
  return new Promise((res) => {
    setTimeout(() => {
      res(i);
    }, 1000);
  });
}

async function assignments(i) {
  elevators.value.floor = await getData(i);
}
watch(elevators.value, (floor) => {
  console.log(`count is: ${floor}`)
})
// watch(elevators.floor, (floor) => {
//   console.log("dfsd")
// })

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
  // let num = Number(f);
  // if (floor) {
  //   elevators.value.isStop[f] = true;
  if (f > floor) {
    for (let i = ++floor; i <= f; i++) {
      console.log("сука1", floor);
      await assignments(i)
      // elevators.value.floor = await getData(i);
    }
    // cleaning(f);
    // console.log(elevators.value.floor);
  } else if (f < floor) {
    for (let i = --floor; i >= f; i--) {
      console.log("сука2", elevators.value.floor);
      await assignments(i)
      // elevators.value.floor = await getData(i);
    }
 } else {
  return
    // console.log("Привет, пользователь!");
  }
}

async function increase(f) {
  // await nextTick ();
  await increaseFloor(f)
}
// cleaning(f);
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
