<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <div class="flex flex-col min-h-screen bg-weather-primary">
    <router-view />
  </div>
</template>
