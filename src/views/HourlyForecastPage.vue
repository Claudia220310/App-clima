<template>
    <ion-page>
      <ion-header>
        <ion-toolbar>
          <ion-title>Pronóstico por Hora</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-content>
        <hourly-forecast :city="city" />
      </ion-content>
    </ion-page>
</template>
  
<script lang="ts">
  import { defineComponent } from 'vue';
  import HourlyForecast from '../components/HourlyForecast.vue';
  import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
  
  export default defineComponent({
    name: 'HourlyForecastPage',
    components: {
      HourlyForecast,
      IonPage,
      IonToolbar,
      IonHeader,
      IonTitle,
      IonContent,
    },
    data() {
      return {
        city: this.$route.query.city || '',
      };
    },
  });
</script>
  
<style scoped>
</style>
  