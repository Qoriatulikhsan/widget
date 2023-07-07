<template>
  <div class="location-widget border border-gray-300 p-4 mb-4 h-full mt-40 ml-96 mr-96 text-center bg-gray-100 rounded-lg shadow-lg">
    <h2 class="text-xl font-bold mb-4 text-3xl">YOUR LOCATION</h2>
    <div v-if="latitude && longitude">
      <p class="text-base text-gray-900 font-semibold text-xl">Latitude: {{ latitude }}</p>
      <p class="text-base text-gray-900 font-semibold mt-2 text-xl">Longitude: {{ longitude }}</p>
    </div>
    <div v-else>
      <p class="text-base text-gray-600">Finding your location...</p>
    </div>

    <div class="location-input mt-4">
      <label for="latitude" class="block mb-1 text-base font-semibold text-gray-700">Latitude:</label>
      <input type="text" id="latitude" v-model="inputLatitude" class="w-48 px-4 py-2 border border-gray-300 rounded" />
    </div>
    <div class="location-input mt-2">
      <label for="longitude" class="block mb-1 text-base font-semibold text-gray-700">Longitude:</label>
      <input type="text" id="longitude" v-model="inputLongitude" class="w-48 px-4 py-2 border border-gray-300 rounded" />
    </div>

    <button @click="fetchLocationDetails" class="mt-4 py-2 px-4 bg-gray-900 text-white rounded">
      Find Location Details
    </button>

    <div v-if="foundLocation" class="location-details mt-4 text-left">
      <h3 class="text-lg font-semibold mb-2">Location Details</h3>
      <p class="text-base text-gray-600">{{ foundLocation.components.country }}</p>
      <p class="text-base text-gray-600">{{ foundLocation.components.city }}</p>
      <p class="text-base text-gray-600">{{ foundLocation.components.street }}</p>
      <p class="text-base text-gray-600">Postal Code: {{ foundLocation.components.postcode }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      latitude: null,
      longitude: null,
      inputLatitude: '',
      inputLongitude: '',
      foundLocation: null,
    };
  },
  mounted() {
    if (navigator.geolocation) {
      navigator.geolocation.getCurrentPosition(this.getPosition);
    }
  },
  methods: {
    getPosition(position) {
      this.latitude = position.coords.latitude;
      this.longitude = position.coords.longitude;
    },
    async fetchLocationDetails() {
      try {
        const apiKey = '92591005a7b94008909d59a64b6d2a49';
        const latitude = this.inputLatitude || this.latitude;
        const longitude = this.inputLongitude || this.longitude;
        const apiUrl = `https://api.opencagedata.com/geocode/v1/json?q=${encodeURIComponent(
          latitude + ',' + longitude
        )}&key=${apiKey}`;

        const response = await fetch(apiUrl);
        const data = await response.json();

        if (data.results && data.results.length > 0) {
          const location = data.results[0];
          this.foundLocation = location;
          console.log('Location:', location);
          // Do something with the found location data
        }
      } catch (error) {
        console.error('Error fetching location data:', error);
      }
    },
  },
};
</script>

<style scoped>
/* No changes needed for style classes */
</style>
