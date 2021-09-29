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
      :src="country.flags.png"
      class="max-h-40 w-full object-cover border-b"
    />
    <div class="bg-transparent w-full h-32 p-4">
      <p class="text-gray-800 text-lg font-bold mb-2">{{ country.name.common }}</p>
      <p class="text-xs font-semibold">
        Area:
        <span class="font-normal text-gray-500">{{ country.area }}</span>
      </p>
      <p class="text-xs font-semibold">
        Region:
        <span class="font-normal text-gray-500">{{ country.region }}</span>
      </p>
      <p v-if="country.capital" class="text-xs font-semibold">
        Capital:
        <span class="font-normal text-gray-500">{{ country.capital[0] }}</span>
      </p>
      <!-- <p v-if="country.languages" class="text-xs font-semibold">
        Languages:
        <span
          v-for="(value, key, index) in country.languages"
          :key="index"
          class="font-normal text-gray-500"
          >{{value}}, 
        </span>
      </p> -->
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