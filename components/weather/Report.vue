<template>
    <div class="weather" v-if="city">
        <img class="weather-icon" :src="weatherIcon" alt="weather icon">
        <h1 class="temp">{{ temperature }}°C</h1>
        <h2 class="city">{{ city }}</h2>
        <div class="details">
            <div style="display: flex;" class="col">
                <img class="humi" src="https://static-00.iconduck.com/assets.00/humidity-icon-2048x1675-xxsge5os.png">
                <div class="info">
                    <p class="humidity">{{ humidity }}%</p>
                    <p>Humidity</p>
                </div>
            </div>
            <div class="col">
                <img src="https://cdn-icons-png.flaticon.com/512/136/136712.png">
                <div class="info">
                    <p class="wind">{{ windSpeed }} km/h</p>
                    <p>Wind Speed</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const props = defineProps({
    city: {
        type: String,
        default: ''
    }
});

const config = useRuntimeConfig();
const _apiKey = config.public.openweatherApiKey;
const temperature = ref('--');
const humidity = ref('--');
const windSpeed = ref('--');
const weatherIcon = ref('https://static.vecteezy.com/system/resources/previews/024/825/182/non_2x/3d-weather-icon-day-with-rain-free-png.png');

const getWeatherIcon = (weatherCode) => {
    // You can expand this with more weather conditions
    const icons = {
        'Clear': 'https://static.vecteezy.com/system/resources/previews/024/825/182/non_2x/3d-weather-icon-day-with-rain-free-png.png',
        'Clouds': 'https://cdn-icons-png.flaticon.com/512/3222/3222800.png',
        'Rain': 'https://cdn-icons-png.flaticon.com/512/1779/1779940.png',
        'Snow': 'https://cdn-icons-png.flaticon.com/512/1779/1779951.png',
        'Thunderstorm': 'https://cdn-icons-png.flaticon.com/512/1779/1779965.png',
        'Drizzle': 'https://cdn-icons-png.flaticon.com/512/1779/1779955.png',
        'Mist': 'https://cdn-icons-png.flaticon.com/512/1779/1779968.png'
    };
    return icons[weatherCode] || icons['Clear'];
};

const fetchWeather = async () => {
    if (!props.city) return;
    
    try {
        const response = await useFetch(`https://api.openweathermap.org/data/2.5/weather?q=${props.city}&appid=${_apiKey}&units=metric`);
        
        if (response.data.value) {
            const data = response.data.value;
            temperature.value = Math.round(data.main.temp);
            humidity.value = data.main.humidity;
            windSpeed.value = Math.round(data.wind.speed * 3.6); // Convert m/s to km/h
            weatherIcon.value = getWeatherIcon(data.weather[0].main);
        }
    } catch (error) {
        console.error('Error fetching weather:', error);
        temperature.value = '--';
        humidity.value = '--';
        windSpeed.value = '--';
    }
};

// Watch for changes in the city prop
watch(() => props.city, (newCity) => {
    if (newCity) {
        fetchWeather();
    }
}, { immediate: true });
</script>