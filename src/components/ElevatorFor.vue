<script setup>
import { computed, inject } from 'vue'

import InformationBoard from "./InformationBoard.vue";
import ButtonElevator from "./ButtonElevator.vue";

const elevators = inject('elevators')

const props = defineProps(["floor"]);
const emit = defineEmits(['handlerClick'])

// const isCall = ref(false)
// const isCall = () => elevators.floor === props.floor
const isCall = computed(() => {
  return elevators.value.floor === props.floor ? true : false
})

function buttonClick() {
  emit('handlerClick', props.floor)
}

// const emit = defineEmits(['handlerClic'])
// function increaseFloor(f) {
//   // for (let i = floors.value[0]; i <= f; i += 2) {
//   //   floors.value.push(i);
//   // }
//   console.log(f)
// }

</script>

<template>
  <div class="elevator">
   <div class="elevator__cabin">
    <InformationBoard :floor="props.floor" :active="isCall"/>
      <font-awesome-icon
        :icon="['fas', 'elevator']"
        :class="[{ active: isCall }]"
        class="fa-8x icon elevator-icon"
      />
    </div>
    <!-- <p>{{elevators.floor}}</p> -->
    <ButtonElevator @click="buttonClick" :disabled="isCall"/>
  </div>
</template>


<style scoped>
.elevator {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: flex-end;
  /* padding-top: 20px; */
  /* padding-bottom: 20px; */
  border: 1px solid gray;
}

.elevator__cabin {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: end;
  border-right: 1px solid gray;
  padding-top: 20px;
}

.elevator-icon {
  border-top: 1px solid gray;
}

.active {
  background-color: aqua;
}
</style>