<script setup>
const props = defineProps(["floor"]);
</script>

<template>
  <div class="information-board">
    <font-awesome-icon :icon="['fas', 'eject']" />
    <p class="information-board__text">{{ props.floor }}</p>
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
</style>