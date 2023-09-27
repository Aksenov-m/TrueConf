<script setup>

import ShaftContainer from './components/ShaftContainer.vue'
import config from './config/default.json'

const shaft = config.SHAFT
</script>

<template>

  <main class="main">
    <ShaftContainer  v-for="item in shaft" :key="item"/>
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
