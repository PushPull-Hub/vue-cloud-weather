<template>
  <div>
    <div v-if="savedCities.length > 0">
      <div
        v-for="city in savedCities"
        :key="city.id"
        class="city-card"
        @click="goToCityView(city)"
      >
        <h2>{{ city.name }}</h2>
        <p v-if="city.weather">
          {{ city.weather.main.temp }}°C,
          {{ city.weather.weather[0].description }}
        </p>
        <p v-else>Loading weather...</p>
      </div>
    </div>
    <h1 v-else>No locations added</h1>
  </div>
</template>

<script setup>
import axios from "axios";
import { ref } from "vue";
import { useRouter } from "vue-router";

const savedCities = ref([]);
const getCities = async () => {
  if (localStorage.getItem("savedCities")) {
    savedCities.value = JSON.parse(localStorage.getItem("savedCities"));

    const requests = [];
    savedCities.value.forEach((city) => {
      requests.push(
        axios.get(
          `https://api.openweathermap.org/data/2.5/weather?lat=${city.coords.lat}&lon=${city.coords.lng}&appid=7efa332cf48aeb9d2d391a51027f1a71&units=imperial`
        )
      );
    });

    const weatherData = await Promise.all(requests);

    weatherData.forEach((value, index) => {
      savedCities.value[index].weather = value.data;
    });
  }
};

await getCities();

const router = useRouter();
const goToCityView = (city) => {
  router.push({
    name: "cityView",
    params: { state: city.state, city: city.city },
    query: {
      id: city.id,
      lat: city.coords.lat,
      lng: city.coords.lng,
    },
  });
};
</script>
