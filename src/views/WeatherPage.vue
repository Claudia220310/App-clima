<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Detalles del clima</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <weather-details :city="city" />
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import WeatherDetails from '../components/WeatherDetails.vue';
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';

export default defineComponent({
  name: 'WeatherPage',
  components: {
    WeatherDetails,
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
