<script setup>
import config from "../config/default.json";

import ElevatorFor from "./ElevatorFor.vue";

const elevator = config.ELEVATOR;

const props = defineProps(["startFloor"]);

const emit = defineEmits(['handlerClick'])

function handlerClick(f) {
  emit('handlerClick', f)
}

// const evenNumbers = computed(() => {
//     return [...elevator].reverse()
// })
</script>

<template>
  <div class="main__shaft">
    <ElevatorFor
      v-for="(item, index) in elevator"
      :key="item"
      :floor="item"
      @handler-click="handlerClick"
      :startFloor="props.startFloor"
    />
  </div>
</template>


<style scoped>
.main__shaft {
  width: 100%;
  display: flex;
  flex-direction: column;
  flex-flow: column-reverse;
}
</style>