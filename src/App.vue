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

      <!-- loading text -->

      <h1 v-if="showLoader" class="text-lg tracking-widest font-semibold">Loading...</h1>

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
          type="text"
          class="border-none py-2 pl-4 bg-transparent outline-none"
          placeholder="Search Country"
        />
        <span
          @click="search = ''"
          v-if="search"
          class="material-icons cursor-pointer mr-1"
          >close</span
        >
      </div>
    </nav>
    <!-- Nav Ends here -->

    <div class="absolute top-14 left-0 right-0">
      <!-- Sidenav starts here -->
      <aside class="h-screen fixed bg-gray-200 w-40 left-0 px-2">
        <div class="mt-4">
          <span class="text-gray-700">Select Region</span>
          <div class="mt-2 flex flex-col">
            <label
              v-for="r in regions"
              :key="r"
              class="inline-flex items-center"
            >
              <input type="radio" v-model="region" :value="r" />
              <span class="ml-2">{{ r }}</span>
            </label>
          </div>
        </div>
      </aside>
      <!-- Side Nav ends here -->

      <!-- Main Starts here -->
      <div v-if="!showLoader" class="absolute left-40">
        <main
          v-if="countriesData.length > 0"
          class="p-10 flex flex-wrap gap-5 justify-center lg:justify-start"
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
import { onMounted, ref, watch } from "vue";
import Country from "./components/Country.vue";
import axios from "axios";
import { lowerCase } from "lodash";

const regions = [
  "All",
  "Asia",
  "Europe",
  "Oceania",
  "Africa",
  "Americas",
  "Polar",
];

const showLoader = ref(false)
const countriesData = ref({} as any);
const fetchedData = ref({} as any);
const search = ref("");
const region = ref();

// watch search value and load data accordingly
watch(search, searchByName);

// watcher on regions
watch(region, searchByRegion);

function searchByName() {
  // filter data and show
  countriesData.value = fetchedData.value;
  countriesData.value = countriesData.value.filter((d: any) =>
    lowerCase(d.name).includes(lowerCase(search.value))
  );
}

function searchByRegion() {
  countriesData.value = fetchedData.value;
  if (region.value === "All") {
    countriesData.value = fetchedData.value;
    return;
  }
  countriesData.value = countriesData.value.filter(
    (d: any) => lowerCase(d.region) == lowerCase(region.value)
  );
}

onMounted(async () => {
  try {
    showLoader.value = true
    const { data } = await axios.get("https://restcountries.eu/rest/v2/all");
    fetchedData.value = data;
    countriesData.value = data;
    showLoader.value = false
  } catch (error) {
    // Show Error Msg
    console.error(error);
  }
});
</script>

<style>
</style>
