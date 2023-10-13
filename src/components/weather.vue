<template>
  <div>
    <!-- Masthead -->
    <header class="masthead">
      <div class="container px-4 px-lg-5 d-flex h-100 align-items-center justify-content-center">
        <div class="d-flex justify-content-center">
          <div class="text-center">
            <h1 class="mx-auto my-0">Weather Today</h1>
            <br />
            <input type="text" class="btn btn-white btn-outline-light text-capitalize" placeholder="city" id="city" v-model="cityName" @keyup.enter="getWeatherData" />&ensp;
            <button type="button" class="btn btn-white btn-outline-light text-capitalize" @click="getWeatherData">Check</button> <br> <br> <br>
            <div class="container btn btn-outline-light text-capitalize "><br>
              <p v-if="weatherData" class="text-capitalize">
                {{ formatDate(weatherData.dt) }}<br />
                {{ formatTime(weatherData.dt) }}<br />
                Today: {{ formatTemperature(weatherData.main.temp) }}°C <br>
                Next day: {{ formatTemperature(weatherData.main.temp_min) }}°C - {{ formatTemperature(weatherData.main.temp_max) }}°C
              </p>
            </div>
          </div>
        </div>
      </div>
    </header>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      cityName: "",
      weatherData: null,
      weatherForecast: null,
      zipCode: 'https://api.openweathermap.org/data/2.5/weather?q=',
      apiKey: '993c78b7af31d37aab8ea234ee47ba37'
    };
  },
  methods: {
    async getWeatherData() {
      try {
        const response = await axios.get(`${this.zipCode}${this.cityName}&appid=${this.apiKey}&units=metric`);
        this.weatherData = response.data;

        const forecastResponse = await axios.get(`${this.zipCode}${this.cityName}&appid=${this.apiKey}&units=metric&exclude=current,minutely,hourly`);
        this.weatherForecast = forecastResponse.data;
      } catch (error) {
        console.error(error);
      }
    },
    formatTime(timestamp) {
      const date = new Date(timestamp * 1000);
      return date.toLocaleTimeString();
    },
    formatDate(timestamp) {
      const date = new Date(timestamp * 1000);
      return date.toLocaleDateString();
    },
    formatTemperature(tempKelvin) {
      return (tempKelvin).toFixed(2);
    },
  },
};
</script>
