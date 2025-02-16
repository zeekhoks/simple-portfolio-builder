<template>
  <div v-if="isLoading">
    <Loader />
  </div>
  <div v-else>
    <Navbar />
    <div class="mt-20 pt-20 pb-20">
      <LandingPage />
    </div>
  </div>
</template>
<script setup lang="ts">
import { ref, onMounted } from "vue";
import Navbar from "./components/Navbar.vue";
import Loader from "./components/Loader.vue";
import LandingPage from "./components/LandingPage.vue";

const isLoading = ref(true);

onMounted(() => {
  // isLoading.value = false;
  setTimeout(() => {
    isLoading.value = false;
  }, 3000);
});
</script>
<style scoped></style>
