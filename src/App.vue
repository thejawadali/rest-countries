<template>
  <div class="w-full h-screen bg-gray-50">
    <!-- Nav starts here -->
    <nav
      class="
        bg-gray-200
        fixed
        h-14
        top-0
        left-0
        right-0
        z-20
        px-8
        shadow-xl shadow-lg shadow-gray-500
        flex
        justify-between
        items-center
      "
    >
      <h1 class="inline text-lg font-bold">Countries Data</h1>
      <!-- Search -->
      <div
        class="
          bg-white
          border border-gray-300
          rounded-lg
          flex
          justify-between
          items-center
          w-56
        "
      >
        <input
          v-model="search"
          @keypress.enter="searchByName"
          type="text"
          class="border-none py-2 pl-4 bg-transparent outline-none"
          placeholder="Search Country"
        />
        <span
          @click="clearSearch"
          v-if="search"
          class="material-icons cursor-pointer mr-1"
          >close</span
        >
      </div>
    </nav>
    <!-- Nav Ends here -->
    <div class="absolute top-14 left-0 right-0">
      <!-- Sidenav starts here -->
      <aside class="h-screen fixed bg-red-200 w-40 left-0">side nav</aside>
      <!-- Side Nav ends here -->

      <!-- Main Starts here -->
      <div class="absolute left-40">
        <main
          v-if="countriesData.length > 0"
          class="
            w-full
            p-10
            flex flex-wrap
            gap-5
            justify-center
            lg:justify-start
          "
        >
          <Country
            v-for="country in countriesData"
            :key="country.name"
            :country="country"
          ></Country>
        </main>
      </div>
      <!-- Main Ends here -->
    </div>
  </div>
</template>

<script lang="ts" setup>
import { computed, onMounted, ref } from "vue";
import Country from "./components/Country.vue";
import axios from "axios";

const regions = [
  "Asia",
  "Europe",
  "Oceania",
  "Africa",
  "Americas",
  "Polar",
  "Northern Africa",
];
const countriesData = ref({} as any);
const search = ref("uk");
const region = ref("");

function clearSearch() {
  search.value = "";
  fetchAllData();
}

async function searchByName() {
  try {
    const { data } = await axios.get(
      `https://restcountries.eu/rest/v2/name/${search.value}`
    );
    countriesData.value = data;
  } catch (error) {
    // Show Error Msg
    console.error("Error occured " + error);
  }
}

async function searchByRegion() {
  try {
    const { data } = await axios.get(
      `https://restcountries.eu/rest/v2/region/${region.value}`
    );
    countriesData.value = data;
  } catch (error) {
    console.error(error);
  }
}

async function fetchAllData() {
  try {
    const { data } = await axios.get("https://restcountries.eu/rest/v2/all");
    countriesData.value = data;
  } catch (error) {
    // Show Error Msg
    console.error(error);
  }
}

onMounted(() => {
  fetchAllData();
  // searchByName();
});
</script>

<style>
</style>
