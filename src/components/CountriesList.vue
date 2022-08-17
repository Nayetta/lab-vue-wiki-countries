<template>
  <div>
    <!-- wrapper div bootstrap  -->
    <div class="container">
      <div v-if="countries" class="row">
        <div class="row">
          <h1 class="me-3">Country List</h1>
          <div class="col-5" style="max-height: 70vh; overflow: scroll">
            <div class="list-group">
              <router-link
                v-for="(country, index) in countries"
                :key="index"
                :to="`/list/${country.alpha3Code}`"
                class="list-group-item list-group-item-action"
              >
                <img
                  :src="`https://flagpedia.net/data/flags/icon/72x54/${country.alpha2Code.toLowerCase()}.png`"
                  alt=""
                />
                <p>{{ country.name.common }}</p>
              </router-link>
            </div>
          </div>
          <div class="col-5">
            <router-view />
          </div>
        </div>
      </div>

      <div v-else class="row">
        <Spinner text="Loading Countries..." />
      </div>
    </div>
  </div>
</template>

<script>
import Spinner from "../components/SpinnerComp.vue";
export default {
  name: "CountriesList",
  components: { Spinner },
  data() {
    return {
      // definir un valor de dato estilo null para poder recibir la info del API!
      countries: null,
    };
  },
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
      const finalResponse = await response.json(); // console.log(finalResponse);//VERIFICAMOS MEDIANTES UNA LLAMADA A CONSOLA QUE RECIBIMOS LOS DATOS
      this.countries = finalResponse.sort((a, b) => {
        return a.name.common.localeCompare(b.name.common);
      });
    },
  },
  //usamos el created hook per fer la llamada inicial a la base de dades. Afegim el async per asegurarnos que evitem problemes amb la llamada a la API
  // al final no cal que sigui async perque la sincronia l aporta la funció detchCountries, el hook created només s'encarrega de cridar aquesta funció
  created() {
    this.fetchCountries();
  },
};
</script>

<style></style>
