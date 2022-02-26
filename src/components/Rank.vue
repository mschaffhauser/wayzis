<script setup>
import { ref } from 'vue'

defineProps({
  data: Object,
})
function capitalizeFirstLetter(string) {
  string = string.toLowerCase()
  return string.charAt(0).toUpperCase() + string.slice(1);
}
</script>

<template>
  <img
    alt="Vue logo"
    :src="`./../src/assets/ranked-emblems/Emblem_${capitalizeFirstLetter(data.tier)}.png`"
  />
  <h1></h1>
  <h1>{{ data }}</h1>
</template>

<style scoped>
a {
  color: #42b983;
}
</style>
