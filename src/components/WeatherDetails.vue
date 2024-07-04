<template>
  <ion-card v-if="weather && weather.main && weather.weather && weather.coord">
    <ion-card-header>
      <ion-card-title>{{ weather.name }}</ion-card-title>
    </ion-card-header>
    <ion-card-content>
      <p class="weather-info">🌡️ Temperatura: {{ weather.main.temp }} °C</p>
      <p class="weather-info">☁️ Condiciones: {{ weather.weather[0].description }}</p>
      <p class="weather-info">💧 Humedad: {{ weather.main.humidity }}%</p>
      <p class="weather-info">📍 Coordenadas: [{{ weather.coord.lat }}, {{ weather.coord.lon }}]</p>
      <go-back-button />
      <ion-button @click="goToHourlyForecast" class="forecast-button">Pronóstico por hora</ion-button>
    </ion-card-content>
  </ion-card>
  <ion-card v-else>
    <ion-card-content>
      <p>Cargando los detalles...</p>
    </ion-card-content>
  </ion-card>
</template>

<script lang="ts">
import { defineComponent, watch } from 'vue';
import { getWeatherDetails } from '@/services/index';
import { IonButton, IonCard, IonCardContent, IonCardHeader, IonCardTitle } from '@ionic/vue';
import GoBackButton from './goBackButton.vue';

export default defineComponent({
  name: 'WeatherDetails',
  components: {
    IonCard,
    IonCardContent,
    IonButton,
    IonCardHeader,
    IonCardTitle,
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
      weather: null,
    };
  },
  methods: {
    async fetchWeatherDetails() {
      try {
        this.weather = await getWeatherDetails(this.city);
      } catch (error) {
        console.error('Error fetching weather details:', error);
      }
    },
    goToHourlyForecast() {
      this.$router.push({ path: '/hourly-forecast', query: { city: this.city } });
    },
  },
  watch: {
    city: {
      immediate: true,
      handler(newCity) {
        if (newCity) {
          this.fetchWeatherDetails();
        }
      },
    },
  },
});
</script>

<style scoped>
ion-card {
  margin: 20px;
  border-radius: 20px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  background-color: #ffffff;
}

ion-card-header {
  background-color: #4a90e2;
  color: white;
  border-top-left-radius: 20px;
  border-top-right-radius: 20px;
  padding: 10px;
  text-align: center;
}

ion-card-title {
  font-size: 1.5em;
  font-weight: bold;
}

ion-card-content {
  display: flex;
  flex-direction: column;
  gap: 10px;
  padding: 20px;
  font-size: 1.1em;
}

.weather-info {
  display: flex;
  align-items: center;
}

.forecast-button {
  margin-top: 20px;
  background-color: #4a90e2;
  color: white;
}
</style>
