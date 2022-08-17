<template>
  <div v-if="countryInfo" class="border border-secondary rounded p-5">
    <div
      class="mb-4 d-flex flex-column justify-content-center align-items-center"
    >
      <img
        :src="`https://flagpedia.net/data/flags/icon/72x54/${alpha2Code}.png`"
        alt=""
      />
      <h1 class="text-center">{{ countryInfo.name.common }}</h1>
    </div>
    <div class="d-flex flex-row justify-content-center">
      <p class="fw-bold mr-2 pe-5">Capital:</p>
      <ul class="ps-5">
        <li
          class="list-unstyled"
          v-for="(capit, index) in capital"
          :key="index"
        >
          {{ capit }}
        </li>
      </ul>
    </div>
    <hr />

    <div class="d-flex flex-row justify-content-center">
      <p class="fw-bold pe-5">Area:</p>
      <p class="ps-5">{{ countryInfo.area }}km<sup>2</sup></p>
    </div>
    <hr />

    <div class="d-flex flex-row justify-content-center">
      <p class="fw-bold mr-2 pe-5">Borders:</p>
      <ul class="ps-5">
        <span></span>
        <li class="list-unstyled">
          <!-- <li v-for="(border, index) in borders" :key="index"> -->
          <p v-if="countryInfo.borders.length === 0">
            This country has no borders <br />
            Who needs a border when you got the Wu Tang Clan. <br />
            <strong>Wu Tang, unifying societies since 1992!</strong>
          </p>
          <p v-else v-for="(border, index) in countryInfo.borders" :key="index">
            <router-link :to="`/list/${border}`">{{ border }}</router-link>
          </p>
          <!-- <router-link :to="`/list/${border}`">{{ border }}</router-link> -->
        </li>
      </ul>
    </div>
  </div>
  <div v-else class="row">
    <Spinner text="Loading Countries..." />
  </div>
</template>

<script>
import Spinner from "../components/SpinnerComp.vue";

export default {
  components: { Spinner },
  data() {
    return {
      capital: [],
      alphaCode: "",
      borders: [],
      alpha2Code: "",
      countryInfo: null,
    };
  },
  methods: {
    async getCountryByAlphaCode() {
      this.alphaCode = this.$route.params.alpha3Code;
      const response = await fetch(
        `https://ih-countries-api.herokuapp.com/countries/${this.alphaCode}`
      );
      const finalResponse = await response.json();
      this.capital = finalResponse.capital;
      this.borders = finalResponse.borders;
      this.alpha3Code = finalResponse.alpha3Code;
      this.alpha2Code = finalResponse.alpha2Code.toLowerCase();
      this.countryInfo = finalResponse;
    },
  },
  mounted() {
    this.getCountryByAlphaCode();
  },
  computed: {
    countryCode() {
      return this.$route.params.alpha3Code;
    },
  },
  watch: {
    countryCode(newContryCode) {
      this.getCountryByAlphaCode();
    },
  },
};
</script>

<style></style>
