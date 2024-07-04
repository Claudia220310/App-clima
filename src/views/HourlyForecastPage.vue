<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Pronóstico</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <hourly-forecast :city="city" />
      <go-back-button />
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent, watch } from 'vue';
import HourlyForecast from '../components/HourlyForecast.vue';
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import { useRoute } from 'vue-router';
import GoBackButton from '../components/goBackButton.vue';

export default defineComponent({
  name: 'HourlyForecastPage',
  components: {
    HourlyForecast,
    IonPage,
    IonToolbar,
    IonHeader,
    IonTitle,
    IonContent,
    GoBackButton,
  },
  data() {
    return {
      city: '',
    };
  },
  mounted() {
    const route = useRoute();
    watch(
      () => route.query.city,
      (newCity) => {
        this.city = newCity;
      },
      { immediate: true }
    );
  },
});
</script>

<style scoped>
ion-header {
  --background: #4a90e2;
  --color: white;
  text-align: center;
}

ion-toolbar {
  --background: #4a90e2;
}

ion-title {
  text-align: center;
  font-size: 1.5em;
  font-weight: bold;
}

ion-content {
  --background: #f2f2f2;
  padding: 20px;
}

ion-page {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

go-back-button {
  margin-top: 20px;
}
</style>
