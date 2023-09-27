<script setup>
import config from '../config/default.json'

import ElevatorFor from './ElevatorFor.vue'

const elevator = config.ELEVATOR
</script>

<template>
    <div>
        <ElevatorFor v-for="item in elevator" :key="item"/>
    </div>
</template>


<style lang="scss" scoped>

</style>