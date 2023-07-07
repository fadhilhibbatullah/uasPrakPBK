<template>
    <div class="weather-widget">
      <h2 class="widget-title">Weather Widget</h2>
      <div class="location-input">
        <label for="location">Enter Location:</label>
        <input type="text" id="location" v-model="location" />
        <button @click="fetchWeatherData">Get Weather</button>
      </div>
      <div v-if="weatherData" class="weather-data">
        <p class="location">Location: {{ weatherData.name }}</p>
        <p v-if="weatherData.main" class="temperature">
          Temperature: {{ Celcius(weatherData.main.temp) }}°C
        </p>
        <p v-if="weatherData.weather" class="description">
          Weather: {{ weatherData.weather[0].description }}
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
      },
      Celcius(kelvin) {
      return (kelvin - 273.15).toFixed(2);
    }
    }
  };
  </script>
  
  <style scoped>
  .weather-widget {
    border: 1px solid #ccc;
    padding: 20px;
    margin-bottom: 20px;
    text-align: center;
    background-color: #f2f2f2;
  }
  .weather-widget button{
    margin-top: 10px;
    background-color: #0062f6;
    color: white;
    border: none;
    border-radius: 4px;
    font-size: 14px;
    cursor: pointer;
    transition: background-color 0.3s ease;
    font-family: 'poppins';
    margin-left: 2px;
  }
  .weather-widget button:hover{
    background-color: #0452c8;

    }

  
  .widget-title {
    margin-top: 0;
    color: #333;
  }
  
  .location-input {
    margin-bottom: 10px;
  }

  #location{
    margin-left: 2px;

  }
  
  .weather-data {
    margin-top: 10px;
  }
  
  .location {
    font-size: 18px;
    font-weight: bold;
  }
  
  .temperature {
    font-size: 24px;
    color: #ff5722;
  }
  
  .description {
    font-size: 16px;
  }
  </style>