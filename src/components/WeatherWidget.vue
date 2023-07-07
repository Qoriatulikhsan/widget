<template>
  <div class="weather-widget bg-gray-200 border border-gray-300 p-4 mb-4 h-full mt-40 ml-96 mr-96 text-center rounded-md">
    <h2 class="widget-title mt-0 text-black text-5xl font-bold ">Weather Widget</h2>
    <div class="location-input mb-2">
      <label for="location" class="block mt-10 text-3xl font-semibold">Enter Location:</label>
      <input type="text" id="location" v-model="location" class=" py-1 px-2 border border-gray-300 rounded mt-10" />
      <button @click="fetchWeatherData" class="py-1 px-2 bg-gray-900 text-white rounded">Get Weather</button>
    </div>
    <div v-if="weatherData" class="weather-data mt-2">
      <p class="location text-3xl font-bold">Location: {{ weatherData.name }}</p>
      <p v-if="weatherData.main" class="temperature text-2xl font-semibold text-gray-900 mt-3">
        Temperature: {{ weatherData.main.temp }}°C
      </p>
      <p v-if="weatherData.weather" class="description text-base text-gray-900 mt-3">
        Description: {{ weatherData.weather[0].description }}
      </p>
    </div>
    <p v-else>Loading weather data...</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      location: '',
      weatherData: null
    };
  },
  methods: {
    async fetchWeatherData() {
      try {
        const apiKey = 'b7bfca7b27a3485144fea086c50d09dc';
        const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${this.location}&appid=${apiKey}`;

        const response = await fetch(apiUrl);
        const data = await response.json();

        this.weatherData = data;
      } catch (error) {
        console.error('Error fetching weather data:', error);
      }
    }
  }
};
</script>
