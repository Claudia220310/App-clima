<template>
  <ion-card v-if="weather && weather.main && weather.weather && weather.coord">
    <ion-card-header>
      <ion-card-title>{{ weather.name }}</ion-card-title>
    </ion-card-header>
    <ion-card-content>
      <p>Temperatura: {{ weather.main.temp }} °C</p>
      <p>Condiciones: {{ weather.weather[0].description }}</p>
      <p>Humedad: {{ weather.main.humidity }}%</p>
      <p>Coordenadas: [{{ weather.coord.lat }}, {{ weather.coord.lon }}]</p>
      <ion-button @click="goBack">Ir a inicio</ion-button>
    </ion-card-content>
  </ion-card>
  <ion-card v-else>
    <ion-card-content>
      <p>Cargando los detalles...</p>
    </ion-card-content>
  </ion-card>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { getWeatherDetails } from '@/services/index';
import { IonButton, IonCard, IonCardContent, IonCardHeader, IonCardTitle } from '@ionic/vue';

export default defineComponent({
  name: 'WeatherDetails',
  components: {
    IonCard,
    IonCardContent,
    IonButton,
    IonCardHeader,
    IonCardTitle
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
    goBack() {
      this.$router.push('/home');
    },
  },
  created() {
    this.fetchWeatherDetails();
  },
});
</script>

<style scoped>
</style>
