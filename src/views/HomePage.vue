<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>App del clima</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <ion-card>
        <ion-card-content>
          <CityInput @city-selected="selectCity" />
        </ion-card-content>
      </ion-card>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import CityInput from '../components/CityInput.vue';
import { IonCard, IonCardContent, IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';

export default defineComponent({
  name: 'HomePage',
  components: {
    CityInput,
    IonPage,
    IonHeader,
    IonToolbar,
    IonTitle,
    IonContent,
    IonCard,
    IonCardContent
  },
  methods: {
    selectCity(city: string) {
      if (city) {
        this.$router.push({ name: 'Weather', query: { city } });
      } else {
        alert("Por favor, ingrese el nombre de una ciudad.");
      }
    },
  },
});
</script>

<style scoped>
</style>
