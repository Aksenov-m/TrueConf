<script setup>

</script>

<template>
  <button class="button" >
    <font-awesome-icon :icon="['fas', 'circle-dot']" class="fa-xl" />
  </button>
</template>

<style scoped>
.button {
  background-color: transparent;
  width: 100%;
  padding: 0;
  border: none;
  margin-bottom: 15px;
  margin-left: 10px;
  cursor: pointer;
}

.button:hover {
  color: green;
}
</style>