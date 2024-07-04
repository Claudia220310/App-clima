<template>
  <ion-card v-if="forecast">
    <ion-card-header>
      <ion-card-title>Pronóstico por hora para {{ city }}</ion-card-title>
    </ion-card-header>
    <ion-card-content>
      <div v-for="item in forecast.list" :key="item.dt" class="forecast-item">
        <p>{{ new Date(item.dt * 1000).toLocaleTimeString() }} - {{ item.main.temp }} °C - {{ item.weather[0].description }}</p>
      </div>
    </ion-card-content>
  </ion-card>
  <ion-card v-else>
    <ion-card-content>
      <p>Cargando pronóstico...</p>
    </ion-card-content>
  </ion-card>
</template>

<script lang="ts">
import { defineComponent, watch } from 'vue';
import { getHourlyForecast } from '@/services/index';
import { IonCard, IonCardContent, IonCardHeader, IonCardTitle } from '@ionic/vue';

export default defineComponent({
  name: 'HourlyForecast',
  components: {
    IonCard,
    IonCardContent,
    IonCardHeader,
    IonCardTitle,
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
  watch: {
    city: {
      immediate: true,
      handler(newCity) {
        this.fetchHourlyForecast();
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
}

ion-card-title {
  font-size: 1.2em;
  text-align: center;
  font-weight: bold;
}

ion-card-content {
  display: flex;
  flex-direction: column;
  gap: 10px;
  padding: 20px;
}

.forecast-item {
  background-color: #f2f2f2;
  border-radius: 10px;
  padding: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
</style>
