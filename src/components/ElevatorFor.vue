<script setup>
import {
  inject,
  reactive,
  watch,
  onMounted
} from "vue";

import InformationBoard from "./InformationBoard.vue";
import ButtonElevator from "./ButtonElevator.vue";

const elevators = inject("elevators");
const props = defineProps(["floor"]);
const emit = defineEmits(["handlerClick"]);

const isCall = reactive({ count: false });
const isUp = reactive({ count: false });

onMounted(() => {
  if (elevators.floor == props.floor) {
    isCall.count = true;
  }
});

watch(elevators, async() => {
  const startFloor = localStorage.floor ? localStorage.floor : 1;
  isCall.count = elevators.floor == props.floor ? true : false;
  isUp.count = elevators.floor > startFloor && props.floor <= elevators.floor? true : false;
});



function buttonClick() {
  emit("handlerClick", props.floor);
}


</script>

<template>
  <div class="elevator">
    <div class="elevator__cabin">
      <InformationBoard
        :floor="props.floor"
        :active="isCall.count"
        :isUp="isUp.count"
      />
      <font-awesome-icon
        :icon="['fas', 'elevator']"
        :class="[{ active: isCall.count }]"
        class="fa-8x icon elevator-icon"
      />
    </div>
    <ButtonElevator @click="buttonClick" :disabled="isCall.count" />
  </div>
</template>


<style scoped>
.elevator {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: flex-end;
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