<script setup>
import { RouterLink, RouterView } from "vue-router";
import { ref } from "vue";
import Navbar from "./components/Navbar.vue";
import CountriesList from "./views/CountriesList.vue";
</script>

<template>
  <div class="app">
    <Navbar />
    <RouterView />
  </div>
</template>

<style scoped></style>

<!-- <script setup>
  import { onMounted } from "vue";
  import NavBar from "./components/NavBar.vue";
  </script>
  
  <template>
    <div class="app">
      <NavBar />
      <RouterView />
    </div>
  </template> -->
