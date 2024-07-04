<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>App del Clima</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <ion-card>
        <ion-card-content>
          <CityInput ref="cityInput" @city-selected="selectCity" />
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
    IonCardContent,
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
  mounted() {
    this.$refs.cityInput.clearCity();
  },
});
</script>

<style scoped>
ion-header {
  --background: #4a90e2;
  --color: rgb(78, 32, 247);
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
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
}

ion-card {
  margin: 20px;
  border-radius: 20px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.438);
  background-color: #ffffff;
}

ion-card-content {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
}
</style>
