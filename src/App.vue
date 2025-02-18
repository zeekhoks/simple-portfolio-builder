<template>
  <div v-if="isLoading">
    <Loader />
  </div>
  <div v-else>
    <Navbar />
    <div class="mt-20 pt-10">
      <LandingPage />
    </div>
    <div>
      <Experience />
    </div>
    <div>
      <Certification />
    </div>
  </div>
</template>
<script setup lang="ts">
import { ref, onMounted } from "vue";
import Navbar from "./components/Navbar.vue";
import Loader from "./components/Loader.vue";
import LandingPage from "./components/LandingPage.vue";
import Experience from "./components/Experience.vue";
import Certification from "./components/Certification.vue";

const isLoading = ref(true);

onMounted(() => {
  isLoading.value = false;
});
</script>
<style scoped></style>
