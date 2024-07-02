<template>
  <div>
    <CityInput @city-selected="selectCity" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import CityInput from '../components/CityInput.vue';

export default defineComponent({
  name: 'HomePage',
  components: {
    CityInput,
  },
  methods: {
    selectCity(city: string) {
      this.$router.push({ name: 'Weather', query: { city } });
    },
  },
});
</script>

<style scoped>

</style>
