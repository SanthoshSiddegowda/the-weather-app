<template>
    <div class="search">
    <input type="search" v-model="city" placeholder="Enter City Name" spellcheck="false" @input="handleSearch">
    <div v-if="searchResults.length > 0" class="search-results">
      <div 
        v-for="result in searchResults" 
        :key="result.item.name"
        class="search-result-item"
        @click="selectCity(result.item.name)"
      >
        {{ result.item.name }}
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref, onMounted } from 'vue';
import Fuse from 'fuse.js';

const city = ref('');
const cities = ref([]);
const searchResults = ref([]);
const fuse = ref(null);

onMounted(async () => {
  try {
    const response = await fetch('/cities_only.json');
    cities.value = await response.json();
    
    fuse.value = new Fuse(cities.value, {
      keys: ['name'],
      threshold: 0.3,
      includeScore: true
    });
  } catch (error) {
    console.error('Error loading cities:', error);
  }
});

const handleSearch = () => {
  if (!city.value.trim()) {
    searchResults.value = [];
    return;
  }
  searchResults.value = fuse.value.search(city.value);
};

const selectCity = (selectedCity) => {
  city.value = selectedCity;
  searchResults.value = [];
  emit('update:city', selectedCity);
};

const emit = defineEmits(['update:city']);
</script>

<style scoped>
.search {
  position: relative;
  width: 100%;
}

.search-results {
  position: absolute;
  top: 100%;
  left: 0;
  right: 0;
  color: black;
  background: white;
  border: 1px solid #ddd;
  border-radius: 4px;
  max-height: 200px;
  overflow-y: auto;
  z-index: 1000;
}

.search-result-item {
  padding: 8px 12px;
  cursor: pointer;
}

.search-result-item:hover {
  background-color: #f5f5f5;
}
</style>