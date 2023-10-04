<script setup>
import {
  ref,
  watch,
  provide,
  watchEffect,
  watchPostEffect,
  onBeforeMount,
  reactive,
  onUpdated,
  onBeforeUpdate,
  computed,
  onMounted,
  nextTick,
} from "vue";
import ShaftContainer from "./components/ShaftContainer.vue";
import config from "./config/default.json";

const shaft = config.SHAFT;

// const elevators = {
//   floors: [1, 2],
//   isStop: [false, false, false, false, false]
// }

const elevators = reactive({
  floor: 1,
});

const startFloor = reactive({
  count: 1,
});

// const floorUp = reactive({count: null})

// const startFloor = computed(() => {
//   if (localStorage.floor) {
//     return localStorage.floor;
//   } else {
//     return 1;
//   }
// });

// watch(elevators, async() => {
//   await res = 
//   if (localStorage.floor) {
//   startFloor.count = localStorage.floor
// }
// });

// watchEffect(() => {

// // console.log(elevators.floor, response, props.floor)
// // isCall.count = elevators.floor == props.floor ? true : false;
// // floorUp.count = elevators.floor;
// console.log(floorUp.count)
// })
// const isUp = reactive({count: false})

// watchEffect(async() => {
//   const res = await elevators.floor;
//   isUp.count = props.floor <= res ? true : false;
// })
// watch(elevators.value, (floor) => {
//   localStorage.setItem('floor', floor);
//   // localStorage.floor = floor;
// });

onBeforeMount(() => {
  if (localStorage.floor) {
    elevators.floor = localStorage.floor;
  }
});

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
  elevators.floor = await getData(i);
}
// watch(elevators.value, (floor) => {
//   console.log(`count is: ${floor}`);
// });
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
  let floor = elevators.floor;
  // let num = Number(f);
  // if (floor) {
  //   elevators.value.isStop[f] = true;
  if (f > floor) {
    for (let i = ++floor; i <= f; i++) {
      console.log("сук", floor);
      await assignments(i);
      // elevators.value.floor = await getData(i);
    }
    // cleaning(f);
    // console.log(elevators.value.floor);
  } else if (f < floor) {
    for (let i = --floor; i >= f; i--) {
      console.log("сук", elevators.floor);
      await assignments(i);
      // elevators.value.floor = await getData(i);
    }
  } else {
    return;
    // console.log("Привет, пользователь!");
  }
  localStorage.setItem("floor", elevators.floor);
}

async function increase(f) {
  // await nextTick ();
  await increaseFloor(f);
}
// cleaning(f);
</script>

<template>
  <main class="main">
    <p>{{startFloor.count}}</p>
    <ShaftContainer
      v-for="item in shaft"
      :key="item"
      @handler-click="increase"
      :startFloor="startFloor.count"
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
