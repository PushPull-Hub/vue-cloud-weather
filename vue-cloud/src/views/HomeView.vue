<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your VueCloud WeatherApp" />
    <SearchBar />
    <Suspense>
      <template #default>
        <CitiesCard />
      </template>
      <template #fallback>
        <div>Loading cities...</div>
      </template>
    </Suspense>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import HelloWorld from "@/components/HelloWorld.vue";
import SearchBar from "@/components/SearchBar.vue";
import CitiesCard from "@/components/CitiesCard.vue";

export default defineComponent({
  name: "HomeView",
  components: {
    HelloWorld,
    SearchBar,
    CitiesCard,
  },
});
</script>
