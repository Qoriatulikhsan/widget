<template>
  <div id="app" class="text-center">
    <header class="bg-gray-800 py-4">
      <nav>
        <ul class="flex justify-center">
          <li class="mr-2">
            <router-link to="/" class="text-white text-base font-medium hover:underline"></router-link>
          </li>
          <li class="mr-2">
            <router-link to="/weather" class="text-white text-base font-medium hover:underline">Weather</router-link>
          </li>
          <li class="mr-2">
            <router-link to="/location" class="text-white text-base font-medium hover:underline">Location</router-link>
          </li>
          <li class="mr-2">
            <router-link to="/stopwatch" class="text-white text-base font-medium hover:underline">Stopwatch</router-link>
          </li>
          <li class="mr-2">
            <router-link to="/tictactoe" class="text-white text-base font-medium hover:underline">Tic Tac Toe</router-link>
          </li>
          <li>
            <router-link to="/photo" class="text-white text-base font-medium hover:underline">Photo</router-link>
          </li>
        </ul>
      </nav>
    </header>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>

<style>
/* No changes needed for style classes */
</style>
