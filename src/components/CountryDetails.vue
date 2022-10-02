<template>
  <div v-if="countryInfo">
    <img
      :src="`https://flagcdn.com/w320/${countryInfo.alpha2Code.toLowerCase()}.png`"
      alt=""
      class="mb-4"
    />
    <h2>{{ countryInfo.name.common }}</h2>
    <ul class="list-group list-group-flush">
      <li
        class="list-group-item d-flex justify-content-between align-items-center"
      >
        <p class="fw-bold">Capital:</p>

        <p v-if="countryInfo.capital.length === 0">
          Este país no tiene capital
        </p>
        <p v-else>{{ countryInfo.capital[0] }}</p>
      </li>
      <li
        class="list-group-item d-flex justify-content-between align-items-center"
      >
        <p class="fw-bold">Area:</p>
        <p>{{ countryInfo.area }}.km<sup>2</sup></p>
      </li>
      <li class="list-group-item d-flex justify-content-between flex-column">
        <p class="fw-bold">Borders:</p>
        <p v-if="countryInfo.borders.length === 0">No hay países fronterizos</p>
        <RouterLink
          v-else
          :to="`/country/${border}`"
          v-for="(border, index) in countryInfo.borders"
          :key="index"
        >
          {{ border }}
        </RouterLink>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { watch, ref, onMounted, computed } from "vue";
import { useRoute } from "vue-router";

const countryInfo = ref(null);

const route = useRoute();

const getCountryByAlphaCode = async () => {
  const alpha3Code = route.params.alpha3Code;
  const response = await fetch(
    `https://ih-countries-api.herokuapp.com/countries/${alpha3Code}`
  );
  const finalResponse = await response.json();

  const name = finalResponse.name.common;
  const capital = finalResponse.capital[0];
  const area = finalResponse.area;
  const borders = finalResponse.borders;
  const alpha2Code = finalResponse.alpha2Code;

  countryInfo.value = finalResponse;

  return { name, capital, borders, area, alpha2Code, countryInfo };
};

onMounted(() => {
  getCountryByAlphaCode();
});

const countryCode = computed(() => {
  return route.params.alpha3Code;
});

watch(countryCode, (newCountryCode) => {
  getCountryByAlphaCode();
});
</script>

<style></style>
