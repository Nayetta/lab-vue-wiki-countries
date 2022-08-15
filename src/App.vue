<template>
  <div className="app">
    <NavBar />
    <router-view />
    <!-- Es veu la primera pàgina del que hi ha en el router/index.js -->
  </div>
</template>

<script>
// import CountriesList from "./components/CountriesList.vue";
// import CountryDetails from "./components/CountryDetails.vue";
import NavBar from "./components/NavBar.vue";
export default {
  components: {
    NavBar,
    // CountriesList,
    // CountryDetails,
  },
  data: () => ({}),
};
</script>

<style></style>
