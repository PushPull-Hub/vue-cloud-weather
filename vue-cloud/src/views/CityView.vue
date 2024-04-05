<template>
  <div>
    <CityCard :city="{ city }" />

    <button
      @click="addCity"
      class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded-md"
    >
      Add
    </button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { ref } from "vue";
import { useRoute, useRouter } from "vue-router";
import CityCard from "../components/CityCard.vue";

const savedCities: any = ref([]);
const route = useRoute();
const router = useRouter();

export default defineComponent({
  name: "CityView",
  components: {
    CityCard,
  },
  props: {
    city: {
      type: Object,
      default: () => ({}),
    },
  },
  methods: {
    addCity,
  },
});

function generateUniqueId() {
  return Math.random().toString(36).substr(2, 9);
}

const saveCitiesToLocalStorage = () => {
  localStorage.setItem("savedCities", JSON.stringify(savedCities.value));
};

function addCity() {
  const locationObj = {
    id: generateUniqueId(),
    state: route.params.state,
    city: route.params.city,
    coords: {
      lat: route.query.lat,
      lng: route.query.lng,
    },
  };

  savedCities.value.push(locationObj);
  saveCitiesToLocalStorage();

  let query = { ...route.query };
  delete query.preview;
  query.id = locationObj.id;
  router.replace({ query });
}

import { onMounted } from "vue";
onMounted(() => {
  if (localStorage.getItem("savedCities")) {
    const citiesFromLS: any = localStorage.getItem("savedCities");
    savedCities.value = JSON.parse(citiesFromLS);
    console.log("savedCities", savedCities);
  }
});
</script>
