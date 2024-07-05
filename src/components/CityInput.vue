<template>
  <ion-card>
    <ion-card-content>
      <ion-item lines="none">
        <ion-input v-model="cityName" placeholder="Ingrese el nombre de la ciudad"></ion-input>
      </ion-item>
      <ion-button expand="block" @click="searchCity">Buscar</ion-button>
    </ion-card-content>
  </ion-card>
</template>

<script lang="ts">
import { defineComponent, watch } from 'vue';
import { IonCard, IonCardContent, IonItem, IonInput, IonButton } from '@ionic/vue';
import { useRoute } from 'vue-router';

export default defineComponent({
  name: 'CityInput',
  components: {
    IonCard,
    IonCardContent,
    IonItem,
    IonInput,
    IonButton,
  },
  data() {
    return {
      cityName: '',
    };
  },
  methods: {
    searchCity() {
      if (this.cityName.trim() !== '') {
        this.$emit('city-selected', this.cityName);
      } else {
        alert('Por favor, ingrese el nombre de una ciudad.');
      }
    },
    clearCity() {
      this.cityName = '';
    },
  },
  mounted() {
    const route = useRoute();
    watch(() => route.path, () => {
      this.clearCity();
    });
  },
});
</script>

<style scoped>
ion-card {
  margin: 20px;
  padding: 20px;
  border-radius: 20px;
  background-color: #00204bb7;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.575);
}

ion-item {
  margin-bottom: 15px;
}

ion-input {
  font-size: 1.2em;
}

ion-button {
  --background: #4a90e2;
  --border-radius: 10px;
  --box-shadow: 0 4px 12px rgba(0, 0, 0, 0.541);
  font-weight: bold;
}
</style>
