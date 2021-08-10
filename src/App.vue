<template>
  <div class="w-full h-screen bg-gray-50">
    <nav
      class="
        bg-gray-200
        py-3
        px-8
        shadow-lg shadow-gray-500
        flex
        justify-between
      "
    >
      <h1 class="inline text-lg font-bold">Countries Data</h1>
    </nav>
    <main
      v-if="countriesData.length > 0"
      class="w-full p-10 flex flex-wrap gap-5 justify-center lg:justify-start"
    >
      <Country
        v-for="country in countriesData"
        :key="country.name"
        :country="country"
      ></Country>
    </main>
  </div>
</template>

<script lang="ts" setup>
import { computed, onMounted, ref } from "@vue/runtime-core";
import Country from "./components/Country.vue";
const countriesData = ref({} as any);
const search = ref("");

function Search() {
  fetch(`https://restcountries.eu/rest/v2/name/${search.value}`)
    .then((res) => res.json())
    .then((res) => {
      console.log("data loaded");
      countriesData.value = res;
    });
}


onMounted(() => {
  // fetch("https://restcountries.eu/rest/v2/region/europe")
  fetch("https://restcountries.eu/rest/v2/all")
    .then((res) => res.json())
    .then((res) => {
      console.log("data loaded");
      countriesData.value = res;
    });
});
</script>

<style>
</style>
