<template>
  <div class="photo-widget bg-gray-200 border border-gray-900 p-4 mb-4 h-full mt-40 ml-96 mr-96 flex flex-col items-center">
    <h2 class="text-3xl font-semibold mb-5 font-serif">{{ title }}</h2>
    <div class="photo-container w-full max-w-md mt-4">
      <img :src="photoUrl" :alt="title" class="max-w-full max-h-full">
    </div>
    <button @click="getRandomPhoto" class="mt-4 py-2 px-4 bg-gray-900 text-white rounded">Load New Photo</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      photoUrl: '',
    };
  },
  mounted() {
    this.getRandomPhoto();
  },
  methods: {
    async getRandomPhoto() {
      try {
        const apiKey = '38037020-2c48722c03be8437a05b588e6';
        const apiUrl = `https://pixabay.com/api/?key=${apiKey}&q=nature&image_type=photo&orientation=horizontal`;

        const response = await fetch(apiUrl);
        const data = await response.json();

        const randomIndex = Math.floor(Math.random() * data.hits.length);
        const randomPhoto = data.hits[randomIndex];

        this.title = randomPhoto.tags;
        this.photoUrl = randomPhoto.webformatURL;
      } catch (error) {
        console.error('Error fetching random photo:', error);
      }
    },
  },
};
</script>


