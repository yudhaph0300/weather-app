<template>
  <div class="app-container">
    <WeatherDisplay />
  </div>
</template>

<script>
import WeatherDisplay from "@/components/WeatherDisplay.vue"; // Update the import

export default {
  components: {
    WeatherDisplay,
  },
};
</script>

<style scoped>
.app-container {
  background-image: url("https://images.unsplash.com/photo-1510987836583-e3fb9586c7b3?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80");
}
</style>
