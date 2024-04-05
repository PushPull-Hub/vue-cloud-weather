<template>
  <div class="weather-secondary">
    <div class="flex justify-between items-center mb-2">
      <h2 class="text-lg font-semibold">{{ city.name }}</h2>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "CityCard",
  props: {
    city: {
      type: Object,
      default: () => ({}),
    },
  },
});
</script>
