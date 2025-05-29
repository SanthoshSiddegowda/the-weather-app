<template>  
<div class="weather-card">
  <WeatherSearch v-model:city="selectedCity" />
  <WeatherReport :city="selectedCity" />
</div>
</template>
<script setup>
import { ref } from 'vue';

const selectedCity = ref('');
</script>
<style>
    @import url("https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.2/font/bootstrap-icons.min.css");
    @import url("~/assets/css/main.css");
</style>