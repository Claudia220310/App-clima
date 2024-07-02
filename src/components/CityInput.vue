<template>
  <div>
    <input type="text" v-model="cityName" placeholder="Ingrese el nombre de la ciudad" />
    <button @click="searchCity">Buscar</button>
  </div>
</template>

<script lang="ts">
// eslint-disable-next-line @typescript-eslint/no-unused-vars
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'CityInput',
  data() {
    return {
      cityName: '',
    };
  },
  methods: {
    searchCity() {
      this.$emit('city-selected', this.cityName);
    },
  },
});
</script>

<style scoped>

</style>
