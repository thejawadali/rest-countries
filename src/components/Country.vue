<template>
  <div class="overflow-hidden shadow-lg rounded-md h-90 w-80 cursor-pointer m-auto bg-white active:bg-gray-100">
    <img
      alt="flag photo"
      :src="country.flag"
      class="max-h-40 w-full object-cover border-b"
    />
    <div class="bg-transparent w-full h-20 p-4 flex items-center">
      <p class="text-gray-800 text-lg font-bold mb-2">{{ country.name }}</p>
    </div>
  </div>
</template>

<script lang="ts">
import { toRefs } from 'vue'


export default{
  props: ["country"],
  setup(props: Readonly<{ country: any}>) {
    const {country} = toRefs(props)
  }
}
</script>