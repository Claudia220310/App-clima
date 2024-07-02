<template>
    <div v-if="forecast && forecast.list">
      <div v-for="hour in forecast.list" :key="hour.dt" class="hourly-forecast">
        <h2>{{ new Date(hour.dt * 1000).toLocaleTimeString() }}</h2>
        <p>Temperatura: {{ hour.main.temp }} °C</p>
        <p>Condiciones: {{ hour.weather[0].description }}</p>
        <p>Humedad: {{ hour.main.humidity }}%</p>
      </div>
      <go-back-button />
    </div>
    <div v-else>
      <p>Cargando pronóstico por hora...</p>
    </div>
</template>
  
<script lang="ts">
  import { defineComponent } from 'vue';
  import { getHourlyForecast } from '@/services/index';
  import GoBackButton from './goBackButton.vue';
  
  export default defineComponent({
    name: 'HourlyForecast',
    components: {
      GoBackButton,
    },
    props: {
      city: {
        type: String,
        required: true,
      },
    },
    data() {
      return {
        forecast: null,
      };
    },
    methods: {
      async fetchHourlyForecast() {
        try {
          this.forecast = await getHourlyForecast(this.city);
        } catch (error) {
          console.error('Error fetching hourly forecast:', error);
        }
      },
    },
    created() {
      this.fetchHourlyForecast();
    },
  });
</script>
  
<style scoped>
  .hourly-forecast {
    margin-bottom: 20px;
  }
</style>
  