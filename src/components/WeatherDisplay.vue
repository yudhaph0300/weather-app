<template>
  <div class="weather-container">
    <b-row class="mb-4">
      <b-col cols="6">
        <h1 class="text-white" style="text-align: left">Weather App</h1>
      </b-col>
      <b-col cols="6">
        <h1 class="text-white" style="text-align: right">{{ currentTime }}</h1>
      </b-col>
    </b-row>
    <b-row class="mb-2">
      <b-col cols="6" md="3" sm="6" class="mx-auto mb-2">
        <b-card>
          <p><strong>Location</strong></p>
          <b-icon
            icon="geo-alt-fill"
            variant="primary"
            font-scale="2"
            class="mb-3"
          ></b-icon>
          <p class="mb-0">
            {{ weather ? `${weather.name}, ${weather.sys.country}` : "" }}
          </p>
        </b-card>
      </b-col>
      <b-col cols="6" md="3" sm="6" class="mx-auto mb-2">
        <b-card>
          <p><strong>Temperature</strong></p>
          <b-icon
            icon="thermometer-half"
            variant="primary"
            font-scale="2"
            class="mb-3"
          ></b-icon>
          <p class="mb-0">{{ weather ? `${weather.main.temp}` : "" }}°C</p>
        </b-card>
      </b-col>
      <b-col cols="6" md="3" sm="6" class="mx-auto mb-2">
        <b-card>
          <p><strong>Weather</strong></p>
          <b-icon
            icon="cloud-drizzle"
            variant="primary"
            font-scale="2"
            class="mb-3"
          ></b-icon>
          <p class="mb-0">
            {{ weather ? `${weather.weather[0].description}` : "" }}
          </p>
        </b-card>
      </b-col>
      <b-col cols="6" md="3" sm="6" class="mx-auto mb-2">
        <b-card>
          <p><strong>Wind Speed</strong></p>
          <b-icon
            icon="wind"
            variant="primary"
            font-scale="2"
            class="mb-3"
          ></b-icon>
          <p class="mb-0">{{ weather ? `${weather.wind.speed}` : "" }} m/s</p>
        </b-card>
      </b-col>
    </b-row>
    <b-row>
      <b-col cols="12" class="mx-auto">
        <b-input-group>
          <b-form-input
            v-model="city"
            @keyup.enter="getWeather"
            placeholder="Enter your country or city..."
          />
          <b-input-group-append>
            <b-button variant="primary" @click="getWeather"
              >Get Weather</b-button
            >
          </b-input-group-append>
        </b-input-group>
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  name: "WeatherDisplay",
  data() {
    return {
      currentTime: "",
      city: "Indonesia",
      weather: null,
      apiKey: process.env.VUE_APP_API_KEY,
    };
  },
  mounted() {
    this.updateTime();
    setInterval(this.updateTime, 1000);

    this.getWeather();
  },
  methods: {
    updateTime() {
      this.currentTime = new Date().toLocaleTimeString();
    },
    getWeather() {
      this.$http
        .get(
          `http://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=${this.apiKey}`
        )
        .then((response) => {
          this.weather = response.data;
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>

<style scoped>
.weather-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 100vh;
  text-align: center;
  padding: 0 10%;
}

@media (max-width: 576px) {
  .weather-container {
    padding: 0 5%;
  }
}
</style>
