<template>
  <div
    class="
      overflow-hidden
      shadow-lg
      rounded-md
      h-90
      w-80
      cursor-pointer
      m-auto
      bg-white
      active:bg-gray-100
    "
  >
    <img
      alt="flag photo"
      :src="country.flag"
      class="max-h-40 w-full object-cover border-b"
    />
    <div class="bg-transparent w-full h-36 p-4">
      <p class="text-gray-800 text-lg font-bold mb-2">{{ country.name }}</p>
      <p class="text-xs font-semibold">
        Population:
        <span class="font-normal text-gray-500">{{ country.population }}</span>
      </p>
      <p class="text-xs font-semibold">
        Region:
        <span class="font-normal text-gray-500">{{ country.region }}</span>
      </p>
      <p class="text-xs font-semibold">
        Capital:
        <span class="font-normal text-gray-500">{{ country.capital }}</span>
      </p>
      <p v-if="country.borders.length > 0" class="text-xs font-semibold">
        Neighbours:
        <span
          v-for="i in country.borders"
          :key="i"
          class="font-normal text-gray-500"
          >{{ i }},
        </span>
      </p>
      <p v-else class="text-xs font-semibold">
        No Neighbour
      </p>
    </div>
  </div>
</template>

<script lang="ts">
import { toRefs } from "vue";

export default {
  props: ["country"],
  setup(props: Readonly<{ country: any }>) {
    const { country } = toRefs(props);
  },
};
</script>