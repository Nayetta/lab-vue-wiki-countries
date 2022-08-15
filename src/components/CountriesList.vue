<template>
  <div>
    <h1>Country List</h1>
    <h2 v-for="country in countries" :key="index">
      {{ country.name.common }}
    </h2>
  </div>
</template>

<script>
export default {
  name: "CountriesList",
  data() {
    return {
      // definimos un valor array para recivir la info del API
      countries: null,
    };
  },
  methods: {
    async fetchCountries() {
      const response = await fetch(
        "https://ih-countries-api.herokuapp.com/countries"
      );
      const finalResponse = await response.json();
      this.countries = finalResponse;
    },
  },
  //usamos el created hook per fer la llamada inicial a la base de dades. Afegim el async per asegurarnos que evitem problemes amb la llamada a la API
  created() {
    this.fetchCountries();
  },
};
</script>

<style></style>
