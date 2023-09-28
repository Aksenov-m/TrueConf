<script setup>
import InformationBoard from "./InformationBoard.vue";
import ButtonElevator from "./ButtonElevator.vue";

import { inject } from 'vue'

const floors = inject('floors')

const props = defineProps(["floor"]);
</script>

<template>
  <div class="elevator">
   <div class="elevator__cabin">
    <InformationBoard :floor="props.floor" />
      <font-awesome-icon
        :icon="['fas', 'elevator']"
        class="fa-8x icon elevator-icon"
      />
    </div>
    <p>{{floors[0]}}</p>
    <ButtonElevator />
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
</style>